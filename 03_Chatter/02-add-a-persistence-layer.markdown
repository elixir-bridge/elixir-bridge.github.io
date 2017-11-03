---
layout: page
title: Adding a Persistence layer
published: false
date: 2016-08-04 23:08:17 -0700
position: 2
---

We have a basic chat app working now, but what happens if you reload the page? Poof! Everything is gone. Some history would be nice, wouldn't it?

# Goals

* add a model for chat message
* Understand Elixir's async() call
* save lines of chat to a database

## Steps

### Create the model

First, we'll create and run a migration. Migrations are pieces of code that dreate or change database columns. In Phoenix, we can invoke `mix phx.gen.schema` from the terminal to generate our model, then run the migration:

```bash
mix phx.gen.schema Message messages name:string message:string
mix ecto.migrate
```

TODO: put migration explanation here
If you're not familiar with migrations, check out [the explanation from the Intro to Phoenix curriculum](/02_Suggestotron/15-creating-a-migration.html).

### Save each message as it comes in

Next, we need to save the messages as they come in. In `lib/chatter_web/channels/chat_room_channel.ex`, we can add a call to do it, so the `handle_in/3` method looks like this:

```elixir
def handle_in("new_message", message, socket) do
  Chatter.Repo.changeset(%Chatter.Message{}, message)
    |> Chatter.Repo.insert
  broadcast! socket, "new_message", message
  {:noreply, socket}
end
```

### Make it faster

The above code is OK, but what happens when we have a million people in our channel? All those saves will slow down the request cycle and keep us from handling the traffic efficiently. Elixir has some built in tools for dealing with exactly this situation. Specifically, `Kernel.spawn/3`, which takes a module, a method, and arguments to pass to the method. So we'll change our handler, and add a method:

```elixir
def handle_in("new_message", message, socket) do
  spawn(__MODULE__, :save_message, [message])
  broadcast! socket, "new_message", message
  {:noreply, socket}
end

@doc false
def save_message(message) do
  Chatter.Message.changeset(%Chatter.Message{}, message)
    |> Chatter.Repo.insert
end
```

What this does is spawn an elixir process to do the save, outside of the request cycle. Since we don't need to see the results of the save to broadcast the message, there's no reason to wait for it.

### Display recent messages when a user joins the channel

So, we have some messages saved, but it would be nice to see them when joining the channel. To do that, we have to change the `join/3` method to return a list of messages, and have the front end code parse and display those messages.

First, in order to complete the joining process, we have to send back `{:ok, socket}` from the `join/3` call. We can't send messages through the socket until the joining process has been completed. Instead, we'll send a call to the `gen_server` underlying our channel to send the messages _after_ the process has completed.

We can handle this by using generic elixir with `send/2`. Let's update our `join/3` message to send the message of `:after_join` in our `join/3` method:

```elixir
def join("chat_room:lobby", payload, socket) do
  if authorized?(payload) do
    send(self, :after_join) # <~ add this line
    {:ok, socket}
  else
    {:error, %{reason: "unauthorized"}}
  end
end
```

Now, we'll need to handle this message using a new handler called `handle_info/2`. Let's add this to our gen_server:

```elixir
def handle_info(:after_join, socket) do
  {:noreply, socket}
end
```

Now this `handle_info/2` will get called after the socket has been connected. We can do anything we want in here. Let's fetch the most recent messages and send them (one-by-one) to our client socket.

### Fetching most recent messages

Since we're going to be getting these messages a lot, it makes sense to put that code in the schema for messages, `lib/chatter/message.ex`. We can add the folloing method to our module, after the `changeset/2` method:

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

Next, we need to broadcast the messages to the channel. `Enum.each/2` will let us step through each item in the collection and reply with the `push/3` method:

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

This should now work. When we reload the page, we should see some recent messages in the chat history. It's not a very neat method at this point though. Something easy to take out, since it's already in it's own closure, is the formatting of the message.

First, let's add another method, `format_msg/1`:

```elixir
defp format_msg(msg) do
  %{
    name: msg.name,
    message: msg.message
  }
end
```

Then, we can replace the formatting in our function in each:

```elixir
  def handle_info(:after_join, socket) do
    Chatter.Message.recent_messages()
    |> Enum.each(fn msg -> push(socket, "new_message", format_msg(msg)) end)
    {:noreply, socket}
  end
```
