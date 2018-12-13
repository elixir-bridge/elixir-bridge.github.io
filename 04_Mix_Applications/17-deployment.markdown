---
layout: page
title: Deployment
date: 2016-10-1 13:38:30 -0700
---

## Deployment

For deployment we will use [distillery](https://hex.pm/packages/distillery). It builds releases of your mix projects.

Open up our `mix.exs` file.

Let's add the following dependency.


defp deps do
  [
    {:distillery, "~> 1.5"},
  ]
end


Our dependencies should now look like this -

```elixir
  defp deps do
    [
      {:cowboy, "~> 2.6"},
      {:plug, "~> 1.7"},
      {:plug_cowboy, "~> 2.0"},
      {:httpoison, "~> 1.4"},
      {:poison, "~> 4.0"},
      {:distillery, "~> 2.0"},
      {:earmark, "~> 1.3", only: :dev},
      {:ex_doc, "~> 0.19.1", only: :dev}
    ]
  end
```

We'll run our `mix deps.get` command to retrieve our dependencies.

### Configure Distillery

To configure distillery we'll run the following command -

```elixir
mix release.init
```


