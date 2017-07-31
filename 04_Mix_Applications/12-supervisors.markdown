## Supervisor

As erlang needs to be reliable system for applications, so built-in to the OTP (Open Telecom Platform) library is the idea of supervision for processes.

You can think of a process as a small self-contained program.
Supervisor is a process which watches over other processes (referred to as child processes).

We can take advantage of this functionality by creating something called a supervision tree. We will take a look at what that means.

First let's look at how we can set up a Supervisor. 
In our `myapp.ex` file located in our lib directory - we are going to add the following snippet.

```elixir
defmodule Myapp do
  use Application
  def start(_type, _args) do
    import Supervisor.Spec, warn: false
    children = [
      worker(Myapp.Router, [])
    ]
    opts = [
      strategy: :one_for_one, name: Myapp.Supervisor
    ]
    Supervisor.start_link(children, opts)
  end
end
```
When our supervisor starts it will call a function `start_link`. This function takes two arguements. `children` and  `options`.

The `children` are the processes that the Supervisor will watch. 

In the `options` arugement, we also need to specify a strategy. This tells the supervisor what to do if a child process fails. 

In this case we are using teh `:one_for_one` strategy. With this process, if the child process terminates, it will be restarted.

Now let's create our router that will handle our requests. 

### Start application on Boot

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



 