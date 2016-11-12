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

# Start the server
$ cd chatter
$ mix phoenix.server

Point your browser to localhost:4000, it should look like this:

Phoenix Chat Markup Screenshot

Setting up a new Channel

### What is a channel

A channel is persisted connection between teh browser and the server. A regular request is like sending letters back and forth between the browser and the server. But a socket is more like a pipe or a phone call. Where the connection is always one, and each side can communicate messages efficiently and quickly. In our case, the server can broadcast messaged down and the users can send messages up through their browser.

* Down means towards the Clients
* Up means towards the server


In a normal request the server only sends one response. But in the case of web sockets the server can continue to send updates as long as the browser maintains the connections.


So channels use websockets.

We’re going to create a new channel called elixirbridge. Open up `web/channels/user_socket.ex` and add this line:


`channel "elixirbridge", Chatter.ElixirBridgeChannel`

Create a new file called web/channels/elixirbridge_channel.ex and implement the functionality for the new elixirbridge channel.

elixir_bridge_channel.ex is analagous to a controller in Phoenix, except it is for handling websocket requests instead of http requests.



Looking at the code below

`channel "elixirbridge", Chatter.ElixirBridgeChannel`

`channel` above refers to the channel method in phoenix. It takes a topic (which is just a namespace). In our case the name space is "elixirbridge"

The next argument `Chatter.ElixirBridgeChannel` is made up of two parts. The first part `Chatter` is the name of the app. The second part `ElixirBridgeChannel` is the name of the module that handles the elixirbridge channel.

The file we're in, `user_channels.ex`, is like the `router.ex` file, but for channels. The topic, in our case `elixirbridge` allows clients to subscribe to the channel. In the same way a path in a web request directs the request the right controller, the topic directs the socket to rhe right module, in this case, `Chatter.ElixirBridgeChannel`.  


In our `web/channels/elixirbridge_channel.ex` paste the following

```
defmodule Chatter.ElixirBridgeChannel do
  use Phoenix.Channel

  def join("elixirbridge", _payload, socket) do
    {:ok, socket}
  end

  def handle_in("new_message", payload, socket) do
    broadcast! socket, "new_message", payload
    {:noreply, socket}
  end
end
```


The join method is a call back that you implement.

If you look at the file, when you call `use Phoenix.Channel` as seen above, it adds a bunch of methods from the Phoenix.channel module. Those methods are called by the router we implemented in the previous step.

The Phoenix.Channel module includes a bunch of extra code, but we still have to define what happens when a client joins the channel, and what happens when someone sends a message to the channel.

First, let's look at the `join/3` method. First, `def join("elixirbridge", _payload, socket) do`: it takes three arguments. The name of the channel, `"elixirbridge"`, is so that this method is only called when the client is joining that specific channel. The second argument, `_payload` is the request from the user. In this case, we're not using it, so we put an underscore in front, to tell the compiler not to worry about it. Finally, it takes `socket`, which is the websocket connection. Then, `{:ok, socket}` just returns a status and the websocket they are connecting to. `join/3` always returns {:ok, socket} to allow all connections to the channel.


Next, let's look at the `handle_in/3` method. It takes an event, a payload and a socket. The event, in this case, will always be `"new_message"`. The payload is the message itself, and the socket is the same websocket from the client connection that they got when they joined. The first line calls `broadcast!/3`. `broadcast!` sends the message to everyone on the channel. The second line returns a status (`:noreply`) and returns the socket as well.  


This for pubsub but for the web. Clients subscribe to something that they want to know about, and when an event happens it is rebroadcast to all the clients

> Publish–subscribe or "pubsub" is a messaging pattern where senders of messages, called publishers, do not program the messages to be sent directly to specific receivers, called subscribers, but instead characterize published messages into classes without knowledge of which subscribers. Similarly, subscribers express interest in one or more classes and only receive messages that are of interest, without knowledge of which publishers.
-wikipedia (https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern)[https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern]


In our app, the clients are both the publishers and the subscribers. You publish a message when you want to say something, and you're also subscribed, listening for messages from anyone else in the channel.

The handle_in method is fired every time a new incoming message is received on the socket, which broadcasts that message to all other open sockets. When you send a message to the chatroom, the chatroom(our channel) sends it back to you and to everyone else in the channel


#TODO page breaks


Handling the connections on Client-side
To make things easier, we’ll start by adding jQuery to our web/templates/layouts/app.html.eex:


<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.2.4/jquery.min.js"></script>
<script src="<%= static_path(@conn, "/js/app.js") %>"></script>

Phoenix comes packed with a simple javascript socket client, but it’s disabled by default. Go into your web/static/js/app.js and uncomment the last line:

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
    channel.push('new_message', { name: name.val(), message: message.val() });
    message.val('');
  }
});

channel.on('new_message', payload => {
  list.append(`<b>${payload.name || 'Anonymous'}:</b> ${payload.message}<br>`);
  list.prop({scrollTop: list.prop("scrollHeight")});
});

channel.join()
  .receive("ok", resp => { console.log("Joined successfully", resp) })
  .receive("error", resp => { console.log("Unable to join", resp) })

// ...

```

`socket.channel("elixirbridge", {})` sends the join request to the server. It makes it's way to the join method we wrote above, and then you get back a websocket.

#Todo
look up what `socket.channel` does

Here, we listen for a keypress event on the message text field. Whenever the user enters a message, it’s pushed on the channel and the text field is cleared. When there’s an incoming message on the channel, it’s appended to the div we previously created and scrolled to the bottom.


Creating the View

Let’s start with something easy by writing the markup and CSS for our chat app. Open web/templates/page/index.html.eex, and replace its contents with:

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
