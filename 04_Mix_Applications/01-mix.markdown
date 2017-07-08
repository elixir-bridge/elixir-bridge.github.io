---
layout: page
title: Modules
date: 2016-10-1 13:38:30 -0700
---

## Mix

A build tool for elixir to building elixir apps.  If you’re familiar with Ruby, Mix is Bundler, RubyGems, and Rake combined.

## Creating our first Project

Type the following into the terminal:

```elixir
mix new myapp
```

You will see the follwing:

```elixir
Annas-MacBook-Pro-3:elixirbridge an$ mix new myapp
* creating README.md
* creating .gitignore
* creating mix.exs
* creating config
* creating config/config.exs
* creating lib
* creating lib/myapp.ex
* creating test
* creating test/test_helper.exs
* creating test/myapp_test.exs

Your Mix project was created successfully.
You can use "mix" to compile it, test it, and more:

    cd myapp
    mix test

Run "mix help" for more commands.

```

If we open our app in an editor we will see the `Mix.exs` file in the root directory. It will look something like this. 

```elixir
defmodule Myapp.Mixfile do
  use Mix.Project

  def project do
    [app: :myapp,
     version: "0.1.0",
     elixir: "~> 1.4",
     build_embedded: Mix.env == :prod,
     start_permanent: Mix.env == :prod,
     deps: deps()]
  end

  # Configuration for the OTP application
  #
  # Type "mix help compile.app" for more information
  def application do
    # Specify extra applications you'll use from Erlang/Elixir
    [extra_applications: [:logger]]
  end

  # Dependencies can be Hex packages:
  #
  #   {:my_dep, "~> 0.3.0"}
  #
  # Or git/path repositories:
  #
  #   {:my_dep, git: "https://github.com/elixir-lang/my_dep.git", tag: "0.1.0"}
  #
  # Type "mix help deps" for more examples and options
  defp deps do
    []
  end
end
```

`def project` defines what is needed in order for your application to compile. 

`def application` defines what is needed for your application to run.

`defp deps` defines the dependencies that are required for the application.







