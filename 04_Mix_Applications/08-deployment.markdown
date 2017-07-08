## Deployment

For deployment we will use [distillery](https://hex.pm/packages/distillery). It builds releases of your mix projects.

Open up our `mix.exs` file.

Let's add the follwing dependency.


defp deps do
  [
    {:distillery, "~> 1.4"},
  ]
end


Our dependencies should now look like this - 

```elixir
 defp deps do
    [
      {:cowboy, "~> 1.1"},
      {:plug, "~> 1.3"},
      {:distillery, "~> 1.4"}
    ]
  end
```

We'll run our `mix deps.get` command to retrieve our dependencies.

To configure distillery we'll run the following command - 

```elixir
mix release.init
```


Since we want our application to start at run time, we need to add a configuration to our `mix.exs` file.

We will add the following to our application 

```elixir
  mod: {Myapp, []}
```

So our applicaion function now looks like:

```elixir
  def application do
    # Specify extra applications you'll use from Erlang/Elixir
    [
      extra_applications: [:logger, :cowboy, :plug],
      mod: {Myapp, []}
    ]
  end
```

Notice that we specify the name of our App as what we pass to the `mod` option. This will start application when it to run. 

