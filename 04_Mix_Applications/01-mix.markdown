---
layout: page
title: Mix
date: 2016-10-1 13:38:30 -0700
---

## Mix

A build tool for elixir to building elixir apps.  If you’re familiar with Ruby, think about Mix as Bundler, RubyGems, and Rake combined.

## Creating our first Project

Type the following into the terminal:

```elixir
mix new my_app --sup
```

You will see the follwing:

```bash
$ mix new my_app
* creating README.md
* creating .formatter.exs
* creating .gitignore
* creating mix.exs
* creating config
* creating config/config.exs
* creating lib
* creating lib/my_app.ex
* creating test
* creating test/test_helper.exs
* creating test/my_app_test.exs

Your Mix project was created successfully.
You can use "mix" to compile it, test it, and more:

    cd my_app
    mix test

Run "mix help" for more commands.

```

## Mix.exs

If we open our app in an editor we will see the `Mix.exs` file in the root directory. This file contains the project information/build instructions for our app.

 It will look something like this.

 ```elixir
defmodule MyApp.MixProject do
  use Mix.Project

  def project do
    [
      app: :my_app,
      version: "0.1.0",
      elixir: "~> 1.6",
      start_permanent: Mix.env() == :prod,
      deps: deps()
    ]
  end

  # Run "mix help compile.app" to learn about applications.
  def application do
    [
      extra_applications: [:logger]
    ]
  end

  # Run "mix help deps" to learn about dependencies.
  defp deps do
    [
      # {:dep_from_hexpm, "~> 0.3.0"},
      # {:dep_from_git, git: "https://github.com/elixir-lang/my_dep.git", tag: "0.1.0"},
    ]
  end
end
```

`def project` defines what is needed in order for your application to compile.

`def application` defines what is needed for your application to run.

`defp deps` defines the dependencies that are required for the application.







