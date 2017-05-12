---
layout: page
title: Creating a Chat App
date: 2016-08-04 23:08:17 -0700
position: 1
---

#### Building a Simple Chat App With Elixir and Phoenix

In this curriculum with will build a simple chat app that takes advantage of phoenix's easy uses of web sockets and evented programming


### Goals:

Through this app we will:

* gain a better understanding of web sockets
* learn how to take advantage of Elixir's Asychronous programming model

Getting Started


```
# Create a new Phoenix project called chatter
$ mix phoenix.new chatter
```

# Prepare the app for the first start

There are a few more steps to get our app ready for the first start. First, we need ot get into or project directory. Then, we need to create the database that we'll use later. For now, it's enought that it exists.

```bash
cd chatter
npm install
mix ecto.create
```

Once you've copied these commands, you should see output like the following:

```bash
02:08:16 matt@pelican
 ~/p/e/chatter>  mix ecto.create
The database for Chatter.Repo has been created
02:22:48 matt@pelican
 ~/p/e/chatter> npm install
npm WARN prefer global coffee-script@1.10.0 should be installed with -g

> fsevents@1.1.1 install /Users/matt/projects/elixirbridge/chatter/node_modules/fsevents
> node install

[fsevents] Success: "/Users/matt/projects/elixirbridge/chatter/node_modules/fsevents/lib/binding/Release/node-v51-darwin-x64/fse.node" is installed via remote
/Users/matt/projects/elixirbridge/chatter
├─┬ babel-brunch@6.0.6
│ ├─┬ anymatch@1.3.0
│ │ ├── arrify@1.0.1
│ │ └─┬ micromatch@2.3.11
│ │   ├─┬ arr-diff@2.0.0
│ │   │ └── arr-flatten@1.0.3
│ │   ├── array-unique@0.2.1
│ │   ├─┬ braces@1.8.5
│ │   │ ├─┬ expand-range@1.8.2
# blah blah output nobody reads until they have a dependency issue
```

# Start the server
```
mix phoenix.server
```

Point your browser to localhost:4000, it should look like this:

[Phoenix Chat Markup Screenshot]

## Setting up a new Channel

### What is a channel

A channel is persisted connection between the browser and the server. A regular request is like sending letters back and forth between the browser and the server. But a socket is more like a pipe or a phone call. Where the connection is always on, and each side can communicate messages efficiently and quickly. In our case, the server can broadcast messaged down and the users can send messages up through their browser.

* Down means towards the Clients
* Up means towards the server

In a normal request the server only sends one response. But in the case of web sockets the server can continue to send updates as long as the browser maintains the connections.

So channels use websockets.

## Creating the channel file

Since Phoenix 1.2, there's a built-in mix task for channels that will create files and do some of the boilerplate work for you. The command is `mix phoenix.gen.channel <channel name>`. Try it out:

``` bash
~/p/e/chatter>  mix phoenix.gen.channel chat_room
* creating web/channels/chat_room_channel.ex
* creating test/channels/chat_room_channel_test.exs

Add the channel to your `web/channels/user_socket.ex` handler, for example:

   channel "chat_room:lobby", Chatter.ChatRoomChannel
~/p/e/chatter>
```

At the end of the command, it tells you to add a line to your `web/channels/user_socket.ex` file. You need to do this so the websocket request can be directed to your channel.


`chat_room_channel.ex` is analagous to a controller in Phoenix, except it is for handling websocket requests instead of http requests.

Looking at the code below,

`channel "chat_room:lobby", Chatter.ChatRoomChannel`

`channel` above refers to the channel method in phoenix. It takes a topic (which is just a namespace for websocket connections). In our case the name space is "chat_room:lobby".

The next argument `Chatter.ChatRoomChannel` is made up of two parts. The first part `Chatter` is the name of the app. The second part `ChatRoomChannel` is the name of the module that handles the elixirbridge channel. In Phoenix, it's conventional to namespace all your modules with your app name first. This helps avoid collisions.

The file we're in, `user_channels.ex`, is like the `router.ex` file, but for channels. The topic, in our case `elixirbridge` allows clients to subscribe to the channel. In the same way a path in a web request directs the request the right controller, the topic directs the socket to rhe right module, in this case, `Chatter.ChatRoomChannel`.  


In our `web/channels/chat_room_channel.ex` paste the following

```elixir
defmodule Chatter.ChatRoomChannel do
  use Chatter.Web, :channel

  def join("chat_room:lobby", payload, socket) do
    if authorized?(payload) do
      {:ok, socket}
    else
      {:error, %{reason: "unauthorized"}}
    end
  end

  # Channels can be used in a request/response fashion
  # by sending replies to requests from the client
  def handle_in("ping", payload, socket) do
    {:reply, {:ok, payload}, socket}
  end

  # It is also common to receive messages from the client and
  # broadcast to everyone in the current topic (chat_room:lobby).
  def handle_in("shout", payload, socket) do
    broadcast socket, "shout", payload
    {:noreply, socket}
  end

  # Add authorization logic here as required.
  defp authorized?(_payload) do
    true
  end
end
```

We now have a bunch of boilerplate code that doesn't look like much, but it will work without modification to hook up to a front end for our simple chat app. Let's look a little closer at what the methods are doing.

First, let's look at the `join/3` method. `def join("chat_room:lobby", payload, socket) do`: it takes three arguments. The name of the channel, `"chat_room:lobby"`, is so that this method is only called when the client is joining that specific channel. The second argument, `payload` is the request from the user; it can contain auth credentials, a message, anything the user wants. Finally, it takes `socket`, which is the websocket connection. There's a test, `authorized?`, which always returns true. Then, `{:ok, socket}` just returns a status and the websocket they are connecting to. `join/3` always returns {:ok, socket} to allow all connections to the channel.

Once a user joins to a channel, then they can send messages to the channel and they'll be received by one of the `handle_in/3` messages. The first one just returns the payload sent by the user back to them. The second one sends the payload to all the users subscribed to the channel. It's this one that allows us to build out chat room with a little front end work. When you send a message to the chatroom, this method sends it back to you and to everyone else in the channel.



Handling the connections on Client-side
To make things easier, we’ll start by adding jQuery to our `web/templates/layouts/app.html.eex:`

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.2.4/jquery.min.js"></script>
<script src="<%= static_path(@conn, "/js/app.js") %>"></script>
```


Phoenix comes packed with a simple javascript socket client, but it’s disabled by default. Go into your `web/static/js/app.js` and uncomment the last line:

```
import socket from "./socket"
```

Go into your web/static/js/socket.js and paste in this:

```
let channel = socket.channel("elixirbridge", {});
let list    = $('#message-list');
let message = $('#message');
let name    = $('#name');

message.on('keypress', event => {
  if (event.keyCode == 13) {
    channel.push('shout', { name: name.val(), message: message.val() });
    message.val('');
  }
});

channel.on('shout', payload => {
  list.append(`<b>${payload.name || 'Anonymous'}:</b> ${payload.message}<br>`);
  list.prop({scrollTop: list.prop("scrollHeight")});
});

channel.join()
  .receive("ok", resp => { console.log("Joined successfully", resp) })
  .receive("error", resp => { console.log("Unable to join", resp) })


```

`socket.channel("elixirbridge", {})` sends the join request to the server, and the server sends the message back to the client.

Here, we listen for a keypress event on the message text field. Whenever the user enters a message, it’s pushed on the channel and the text field is cleared. When there’s an incoming message on the channel, it’s appended to the div we previously created and scrolled to the bottom.


Creating the View

Now we have to write the markup and CSS for our chat app. Open web/templates/page/index.html.eex, and replace its contents with:

```
<div id='message-list' class='row'>
</div>

<div class='row form-group'>
  <div class='col-md-3'>
    <input type='text' id='name' class='form-control' placeholder='Name' />
  </div>
  <div class='col-md-9'>
    <input type='text' id='message' class='form-control' placeholder='Message' />
  </div>
</div>
```
We’ve created an empty div that will list all chat messages and two text fields (one for the user’s name and one for the message).

Now open `web/static/css/app.css `and paste this at the end:

#message-list {
  border: 1px solid #777;
  height: 400px;
  padding: 10px;
  overflow: scroll;
  margin-bottom: 50px;
}


#TODO

Channel persistance - if the server goes down or is reset all the messages will disappear
A nice feature to have would be to share messages across servers

- channels between apps as well

#Todo
something async
