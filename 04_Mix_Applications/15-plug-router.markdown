## Plug.Router

We'll most often use the Plug.Router to match and dispatch requests.

Plug.Router is a plug that contains its own plug pipeline.

When the router is invoked, it will invoke the `:match` plug as we see above which is represented by the `match/2` function we see in our example.

```elixir
defmodule Myapp.Router do
  use Plug.Router
  plug :match
  plug :dispatch

  def start_link() do
    {:ok, _} = Plug.Adapters.Cowboy.http Myapp.Router, [], [port: 4000]
  end

  get "/" do
    conn
      |> send_resp(200, "YAY")
      |> halt
  end
  match _ do
    conn
      |> send_resp(404, "Not found")
      |> halt
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

Let's add parsers to our router - open up the router file and copy the following right below the `:dispatch` function

```elixir
plug Plug.Parsers,
  parsers: [:urlencoded, :multipart, :json],
  pass: ["*/*"],
  json_decoder: Poison
```

Our router should now look like this -

```elixir
defmodule Myapp.Router do
  use Plug.Router

  plug :match
	plug :dispatch

  plug Plug.Parsers, parsers: [:urlencoded, :multipart]
  plug Plug.Parsers, parsers: [:urlencoded, :json],
                   pass:  ["text/*"],
                   json_decoder: Poison


  def start_link() do
    {:ok, _} = Plug.Adapters.Cowboy.http Myapp.Router, [], [port: 4000]
  end

  get "/" do
    conn
      |> put_resp_content_type("text/html")
      |> send_resp(200, page)
      |> halt
  end

  match _ do
    conn
      |> send_resp(404, "Not found")
      |> halt
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

The send_resp function defined on our Plug.Conn, allows us to send response back to our client.

The halt funciton halts the Plug pipeline by preventing further plugs downstream from being invoked.


### Forwarding

```elixir
forward "/hello", to: Myapp.Plugs.HelloWorld
```

`forward` is invoked by Plug.Router to forward requests to another plug.

