---
layout: page
title: Plug.Router
date: 2016-10-1 13:38:30 -0700
---

## Plug.Router

We'll most often use the Plug.Router to match and dispatch requests.

Plug.Router is a plug that contains its own plug pipeline.

When the router is invoked, it will invoke the `:match` plug as we see above, which is represented by the `match/2` function we see in our example.

```elixir
defmodule MyApp.Router do
  use Plug.Router
  plug :match
  plug :dispatch

  def child_spec(_opts) do
    %{
      id: __MODULE__,
      start: {__MODULE__, :start_link, []},
      type: :worker,
      restart: :permanent,
      shutdown: 500
    }
  end

  def start_link() do
    {:ok, _} = Plug.Adapters.Cowboy2.http(MyApp.Router, [], port: 4000)
  end

  match _ do
    conn
    |> send_resp(404, "Not found")
  end
end
```

Thw `match/2` function will check against any of our HTTP requests to see which one matches.

Then it calls the `:dispatch` plug which will execute the matched code.

Our `start_link` function will be called by the Supervisor.


### Supporting APIs

Plug ships with several parsers that our application to parse different content-types.

```elixir
plug Plug.Parsers,
  parsers: [:urlencoded, :multipart, :json],
  pass: ["*/*"],
  json_decoder: Poison
```

We will use Poison, an JSON library for Elixir, to decode JSON.

Let's add parsers to our router - open up the router file and copy the following before the `:dispatch` function

```elixir
plug Plug.Parsers,
  parsers: [:urlencoded, :multipart, :json],
  pass: ["*/*"],
  json_decoder: Poison
```

Our router should now look like this -

```elixir
defmodule MyApp.Router do
  use Plug.Router
  plug :match

  plug Plug.Parsers,
  parsers: [:json],
  pass: ["*/*"],
  json_decoder: Poison

  plug :dispatch

  def child_spec(_opts) do
    %{
      id: __MODULE__,
      start: {__MODULE__, :start_link, []},
      type: :worker,
      restart: :permanent,
      shutdown: 500
    }
  end

  def start_link() do
    {:ok, _} = Plug.Adapters.Cowboy2.http(MyApp.Router, [], port: 4000)
  end

  get "/" do
    conn
    |> send_resp(200, "yay")
    |> halt
  end

  match _ do
    conn
    |> send_resp(404, "Not found")
  end
end
```

### Sending Responses

We will want to be able to send responses to our client.

```elixir
conn
  |> send_resp(200, "Ok")
  |> halt
```

The send_resp function, defined on our Plug.Conn, allows us to send response back to our client.

The halt function halts the Plug pipeline by preventing further plugs downstream from being invoked.


### Forwarding

```elixir
forward "/hello", to: MyApp.Plugs.HelloWorld
```

`forward` is invoked by Plug.Router to forward requests to another plug.

