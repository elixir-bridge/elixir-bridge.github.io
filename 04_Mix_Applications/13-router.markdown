---
layout: page
title: Router
date: 2016-10-1 13:38:30 -0700
---

## Router

Now We are going to create a router that will route requests coming into our application.

Let's create a `router.ex` file in our `lib` directory in our applicaiton.

Type the following into that file:

```elixir
defmodule Myapp.Router do
  use Plug.Router
  plug :match
  plug :dispatch

  def start_link() do
    {:ok, _} = Plug.Adapters.Cowboy.http Myapp.Router, [], [port: 4000]
  end

  match _ do
    conn
      |> send_resp(404, "Not found")
      |> halt
  end
end
```






