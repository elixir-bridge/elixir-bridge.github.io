---
layout: page
title: Deployment
date: 2016-10-1 13:38:30 -0700
---

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

### Configure Distillery

To configure distillery we'll run the following command -

```elixir
mix release.init
```


