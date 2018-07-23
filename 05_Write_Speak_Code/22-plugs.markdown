---
layout: page
title: Plugs
date: 2016-10-1 13:38:30 -0700
---

## Plugs

Notice that we are using the `Plug` module.

Plugs provide a common interface for handling connections. We're going to use plugs extensively throughout our elixir apps.

So what is a Plug?

A plug can take two shapes. A function plug  receives a connection and a set of options as arguments and returns the connection:

Example:

```elixir
def hello_world_plug(conn, _opts) do
  conn
  |> put_resp_content_type("text/html")
  |> send_resp(200, "<h1>Hello world</h1>)
end
```

A module plug implements an init/1 function to initialize options, and a call/2 function which received the intialized options and the connection and returns a connection.

```elixir
defmodule HelloWorldPlug do
  import Plug.Conn
  def init([]), do: false
  def call(conn, _opts), do: conn
end
```

A connection represents a `Plug.Conn` struct which looks like this:

```elixir
%Plug.Conn{host: "elixirbridge.org",
           path_info: ["hello", "world"],
           ...}
```
