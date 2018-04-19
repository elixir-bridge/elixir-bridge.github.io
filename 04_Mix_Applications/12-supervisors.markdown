---
layout: page
title: Supervisors
date: 2016-10-1 13:38:30 -0700
---

## Supervisor

As erlang needs to be reliable system for applications, so built-in to the OTP (Open Telecom Platform) library is the idea of supervision for processes.

You can think of a process as a small self-contained program.
Supervisor is a process which watches over other processes (referred to as child processes).

We can take advantage of this functionality by creating something called a supervision tree. We will take a look at what that means.

First let's look at how we can set up a Supervisor.
In our `myapp.ex` file located in our lib directory - we are going to add the following snippet.

```elixir
defmodule MyApp do
  use Application

  def start(_type, _args) do
    children = [
      {MyApp.Router, []}
    ]

    opts = [strategy: :one_for_one, name: MyApp.Supervisor]
    Supervisor.start_link(children, opts)
  end
end
```

When our supervisor starts it will call a function `start_link`. This function takes two arguments - a list of tuples, and a strategy for how to restart child processes when they fail. Each tuple contains the name of the Child Process, and any initial arguments that will get passed into the start_link function of that respective module.

The `children` are the processes that the Supervisor will watch. The Supervisor will iterate over every child module and find its `child_spec/` which defines how the child will be started, stopped, and restarted. Usually this is with a `start_link/1` function. We will look at the `child_spec` soon.

In the `options` argument, we also need to specify a strategy. This tells the supervisor what to do if a child process fails.

In this case we are using the `:one_for_one` strategy. With this process, if the child process terminates, it will be restarted.

Now let's create our router that will handle our requests.

### Start application on Boot

Since we want our application to start at run time, we need to add a configuration to our `mix.exs` file.

We will add the following to our application

```elixir
  mod: {MyApp, []}
```

So our application function now looks like:

```elixir
  def application do
    [
      extra_applications: [:logger],
      mod: {MyApp, []}
    ]
  end
```

Notice that we specify the name of our App as what we pass to the `mod` option. This is our application callback module. So when our application starts, the module we pass to `mod` will be started
