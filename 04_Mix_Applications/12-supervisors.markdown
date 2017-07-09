## Supervisor

As erlang needs to be reliable system for applications, so built-in to the OTP (Open Telecom Platform) library is the idea of supervision for processes.

You can think of a process as a small self-contained program.
Supervisor is a process which watches over other processes (referred to as child processes).

We can take advantage of this functionality by creating something called a supervision tree. We will take a look at what that means.

First let's look at how we can set up a Supervisor.

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



