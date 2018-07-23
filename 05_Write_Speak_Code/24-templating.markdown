---
layout: page
title: Templating
date: 2016-10-1 13:38:30 -0700
---

## Templating

Elixir allows you to create template files to create views for your web application. EEX stands for embedded elixir and it works like ERB for Ruby or Jinja for Python.

Let's create a `templates` directory

```bash
mkdir templates
```

cd into that directory we'll create a file called `home.html`

```bash
home.html
```

Now let's add the folowing line of code to our `get` route in our router

```elixir
page = EEx.eval_file("templates/home.html")
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
    page = EEx.eval_file("templates/home.html")
    conn
    |> put_resp_content_type("text/html")
    |> send_resp(200, page)
    |> halt
  end

  match _ do
    conn
    |> send_resp(404, "Not found")
  end
end
```

As we can see above, the `eval_file/3` function allows us to retrieve a file name, and evaluate the values using bindings.

We can then send that template back in a response to the client.

### Interpolation

In Eex we can interpolate variables list so:

```elixir
<h2><% name %></h2>
```





