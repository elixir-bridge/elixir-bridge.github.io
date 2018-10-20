---
layout: page
title: Adding a Persistence layer
date: 2016-08-04 23:08:17 -0700
position: 2
---

We have a basic chat app working now, but what happens if you reload the page? Poof! Everything is gone. Some history would be nice, wouldn't it?

# Goals

* Add a schema for chat messages
* Save lines of chat to a database
* Understand asynchronous request handling


## Steps

### Generate the schema

In Phoenix, schemas represent the structures of your database tables. At this point, we have no tables, so we'll use a schema to define one and then run a migration to actually create the table in the database. This is analogous to "models" in other frameworks. Migrations are pieces of code that create or change database structure. 

We have Mix helpers to create the schema definition and then run the migration in the terminal:

```bash
mix phx.gen.schema Message messages name:string message:string
mix ecto.migrate
```

### Save each message as it comes in

Next, we need to save the messages as they come in. In `lib/chatter_web/channels/chat_room_channel.ex`, we can add a call to do it, so the `handle_in/3` function looks like this:

```elixir
def handle_in("new_message", payload, socket) do
  Chatter.Message.changeset(%Chatter.Message{}, payload) |> Chatter.Repo.insert
  
  broadcast! socket, "new_message", payload
  {:noreply, socket}
end
```

### Make it faster

The above code works, but what happens when we have a million people in our channel? Those inserts are happening synchronously. All those saves will slow down the request cycle and keep us from handling the traffic efficiently.

Elixir has some built in tools for dealing with exactly this situation. Specifically, `Kernel.spawn/1`, which takes a function to call, in this case `save_message/1` with our message. So we'll change our handler and add that function:

```elixir
def handle_in("new_message", payload, socket) do
  spawn(fn -> save_message(payload) end)
  broadcast! socket, "new_message", payload
  {:noreply, socket}
end

defp save_message(message) do
  Chatter.Message.changeset(%Chatter.Message{}, message)
    |> Chatter.Repo.insert
end
```

This immediately creates a new process to do the save, outside of the request cycle. Since we don't need to see the results of the save to broadcast the message, there's no reason to wait for it. This change allows our chat app to host a very large number of users all chatting at the same time with their chat being saved to the database.

### Display recent messages when a user joins the channel

So, we have some messages saved, but it would be nice to see them when joining the channel so we have some context on the chat going on. To do that, we have to change the `join/3` function to return a list of messages, and have the message list box on the page display those messages. Unfortunately, we can't send all those messages to the channel we're joining until after the `join/3` function has returned. And by then it's too late.

What to do?

Elixir helps us out here. Under the hood we're working with an Elixir `Process`, and each Elixir process has a mailbox. We're going to send a message to our own process mailbox using the `send/2` function. Then, in the future, our process is going to read it and carry out the instructions it finds there.

In the code below, we use `send/2`, specifying the process mailbox to send the message to -- in this case it's our own process -- and a function to call when it handles the message in the mailbox. This is all going to happen after the `join/3` function is finished and we are fully joined to the channel.

```elixir
def join("chat_room:lobby", payload, socket) do
  if authorized?(payload) do
    send(self(), :after_join)
    {:ok, socket}
  else
    {:error, %{reason: "unauthorized"}}
  end
end
```

Now, we'll need to handle this message using a new handler called `handle_info/2`. This is a callback on `Phoenix.Channel` that takes care of executing calls not related to requests and responses from sockets. Think of it as a catchall for function calls to the channel.

```elixir
def handle_info(:after_join, socket) do
  {:noreply, socket}
end
```

Now this `handle_info/2` will get called after the socket has been connected. We can do anything we want in here. Let's fetch the most recent messages and send them (one-by-one) to our socket.

### Fetching most recent messages

Since we're going to be getting these messages a lot, it makes sense to put that code in the schema for messages, `lib/chatter/message.ex`. We can add the following function to our module, after the `changeset/2` function:

```elixir
def recent_messages(limit \\ 10) do
  Chatter.Repo.all(Chatter.Message, limit: limit)
end
```

This gives us a default of 10 messages, which will work well for our current case.

Now, we can add this to our channel  `handle_info/3` call.

```elixir
def handle_info(:after_join, socket) do
  Chatter.Message.recent_messages()
  {:noreply, socket}
end
```

Next, we need to broadcast the messages to the channel so they show up in the message list. Elixir's `Enum.each/2` will let us step through each message returned by `recent_messages()` and send it as a new message to the channel with the `Channel.push/3` function.

```elixir
def handle_info(:after_join, socket) do
  Chatter.Message.recent_messages()
  |> Enum.each(fn msg -> push(socket, "new_message", %{
    name: msg.name,
    message: msg.message
  }) end)
  {:noreply, socket}
end
```

When we reload the page, we should see 10 recent messages in the chat history.
But there's something about this `handle_info` function that looks cluttered. Let's clean it up a little by separating the message formatting.

First, let's add another private function, `format_msg/1`.

```elixir
defp format_msg(msg) do
  %{
    name: msg.name,
    message: msg.message
  }
end
```

Now let's use that new function by replacing that inline formatting.

```elixir
  def handle_info(:after_join, socket) do
    Chatter.Message.recent_messages()
    |> Enum.each(fn msg -> push(socket, "new_message", format_msg(msg)) end)
    {:noreply, socket}
  end
```

All right, that gives us a better user experience for new folks joining the room.