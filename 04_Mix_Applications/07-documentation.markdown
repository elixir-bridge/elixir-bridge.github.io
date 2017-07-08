## Documentation

Elixir makes documenting our code really straihtforward.

Document a module using `@moduledoc `.
Document function using `@doc`.
Spec a function with `@spec`.

Let's open our our `myapp.ex` file. Add add some documentation. 

```elixir
defmodule Myapp do
  @moduledoc """
    Main application module
  """
  @doc """
  Say hello
  ## Parameters
  - name: String of a person
  ## Examples
    iex> Myapp.say("Ari")
    "Hello Ari"
  """
  @spec say(String.t) :: String.t
  def say(name) do
    "Hello #{name}"
  end
```


To actually add the documentation, we will use two packages `:earmark` and `:ex_doc`. 
[:earmark](https://hex.pm/packages/earmark) is a pure Elixir markdown converter.

[:ex_doc](https://hex.pm/packages/ex_doc) is a documentation generation tool for Elixir.

To generate our documentation we can run `mix docs`

