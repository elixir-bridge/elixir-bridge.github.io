---
layout: page
title: Documentation
date: 2016-10-1 13:38:30 -0700
---

## Documentation

Elixir makes documenting our code really straightforward.

Document a module using `@moduledoc `.
Document function using `@doc`.
Spec a function with `@spec`.

Let's open our our `myapp.ex` file. Add add some documentation.

```elixir
defmodule MyApp do
  @moduledoc """
      Main application module
  """

  @doc """
  Says Hello

  ## Examples

      iex> MyApp.say("Ari")
      "Hello Ari"
  """

  @spec say(String.t()) :: String.t()
  def say(name) do
    "Hello #{name}"
  end
```


To actually add the documentation, we will use two packages `:earmark` and `:ex_doc`.
[:earmark](https://hex.pm/packages/earmark) is a pure Elixir markdown converter.

[:ex_doc](https://hex.pm/packages/ex_doc) is a documentation generation tool for Elixir.

Let's add these dependencies to our Mix.exs file. It should now look like this.

```elixir
defp deps do
  [
    {:cowboy, "~> 2.6"},
    {:plug, "~> 1.7"},
    {:plug_cowboy, "~> 2.0"},
    {:earmark, "~> 1.3", only: :dev},
    {:ex_doc, "~> 0.19.1", only: :dev}
  ]
end
```


Let's retrieve our dependencies using `mix deps.get`

To generate our documentation we can run `mix docs`

To view our documentation we can run `open doc/index.html`
