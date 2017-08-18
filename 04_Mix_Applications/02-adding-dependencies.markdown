---
layout: page
title: Adding dependencies
date: 2016-10-1 13:38:30 -0700
---

## Adding Dependencies

Let's add a dependency. We'll use a package called [cowboy](https://github.com/ninenines/cowboy), an HTTP server for erlang/elixir and one called [plug](https://github.com/elixir-lang/plug), a specification tool and connection adapter for web servers.


Let's open up our Mixfile an add our dependenices.  But first let's look up the latest version for each dependency

Type the function

```elixir
mix hex.info cowboy
```

```elixir
defmodule Myapp.Mixfile do
  # ...
  defp deps do
    [
      {:cowboy, "~> 1.1"},
      {:plug, "~> 1.3"}
    ]
  end
end
```

How do we figure out what version to use? The command `mix hex.info #{dependency}` will get info from the central package repo, called hex.

```bash
$ mix hex.info cowboy
Small, fast, modular HTTP server.

Config: {:cowboy, "~> 1.1"}
Releases: 1.1.2, 1.1.1, 1.1.0, 1.0.4, 1.0.3, 1.0.2, 1.0.1, 1.0.0

Maintainers: Loïc Hoguin
Licenses: ISC
Links:
  GitHub: https://github.com/ninenines/cowboy

```

You can also go to the Hex site and browse packages: [hex.pm](https://hex.pm).


## Installing Dependencies

Mix has a build in command for installing dependencies, `mix deps.get`. Let's pull our dependencies we've just added:

```bash
$ mix deps.get
Running dependency resolution...
Dependency resolution completed:
  cowboy 1.1.2
  cowlib 1.0.2
  mime 1.1.0
  plug 1.3.5
  ranch 1.3.2
* Getting cowboy (Hex package)
  Checking package (https://repo.hex.pm/tarballs/cowboy-1.1.2.tar)
  Fetched package
* Getting plug (Hex package)
  Checking package (https://repo.hex.pm/tarballs/plug-1.3.5.tar)
  Fetched package
* Getting mime (Hex package)
  Checking package (https://repo.hex.pm/tarballs/mime-1.1.0.tar)
  Fetched package
* Getting cowlib (Hex package)
  Checking package (https://repo.hex.pm/tarballs/cowlib-1.0.2.tar)
  Fetched package
* Getting ranch (Hex package)
  Checking package (https://repo.hex.pm/tarballs/ranch-1.3.2.tar)
  Fetched package
```

You'll see that it fetches your dependencies, and also the packages that they depend on.

## Running Dependencies

For dependencies to work, some of them need to be included in the list of applications in your `mix.exs`. We'll change the definition of `application/0`:

```elixir
# mix.exs
def application do
  [extra_applications: [:logger, :cowboy, :plug]]
end
```

Now, when the application is started, it will also start `:cowboy` and `:plug`.
