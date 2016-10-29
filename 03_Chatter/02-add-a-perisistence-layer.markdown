---
layout: page
title: Adding a Persistence layer
date: 2016-08-04 23:08:17 -0700
position: 2
---
We have a basic chat app working now, but what happens if you reload the page? Poof! Everything is gone. Some history would be nice, wouldn't it?

# Goals

* add a model for chat text
* Understand Elixir's async() call
* save lines of chat to a database

## Steps

### Create the model

First, we'll create and run a migration. Migrations are pieces of code that dreate or change database columns. In Phoenix, we can invoke `mix phoenix.gen.model` from the terminal to generate our model, then run the migration:

```
mix phoenix.gen.model Message messages name:string text:string
mix phoenix.migrate
```

If you're not familiar with migrations, check out [the explanation from the Intro to Phoenix curriculum](/02_Suggestotron/15-creating-a-migration.html).

### Save each message as it comes in

Next, we need to save the messages as they come in. In `web/channels/elixirbridge_channel.ex`, we can add a call to do it, so the `handle_in/3` method looks like this:

```
def handle_in("new_message", message, socket) do
  Chatter.Repo.changeset(%Chatter.Message{}, message)
    |> Chatter.Repo.insert
  broadcast! socket, "new_message", message
  {:noreply, socket}
end
```

### Make it faster

The above code is OK, but what happens when we have a million people in our channel? All those saves will slow down the request cycle and keep us from handling the traffic efficiently. Elixir has some built in tools for dealing with exactly this situation. Specifically, `Kernel.spawn/3`, which takes a module, a method, and arguments to pass to the method. So we'll change our handler, and add a method:

```
def handle_in("new_message", message, socket) do
  spawn(__MODULE__, :save_message, message)
  broadcast! socket, "new_message", message
  {:noreply, socket}
end

def save_message(message) do
  Chatter.Repo.changeset(%Chatter.Message{}, message)
    |> Chatter.Repo.insert
end
```

What this does is spawn an elixir process to do the save, outside of the request cycle. Since we don't need to see the results of the save to broadcast the message, there's no reason to wait for it.

### Display recent messages when a user joins the channel

So, we have some messages saved, but it would be nice to see them when joining the channel. To do that, we have to change the `join/2` method to return a list of messages, and have the front end code parse and display those messages.
