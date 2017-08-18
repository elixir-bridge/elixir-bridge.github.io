---
layout: page
title: Modules
date: 2016-10-1 13:38:30 -0700
---

## Modules

In Elixir, we'll be building modules to group functions together. Like other languages, this is used to group common functionality together.

We've already seen this in action when using previous modules, such as `String` and `Float`. We can create custom modules as well using the `defmodule` macro. For instance, let's say we want to create a `Students` module. We can define it like so:

```elixir
defmodule Students do
end
```

The `Students` module isn't very interesting _yet_. We can define functions inside a module using the `def` keyword. For instance, let's say we want to define a `count/0` function which lists the number of students:

```elixir
defmodule Students do
  def count() do
    31
  end
end
```

We can then call the `Students.count/0` function just like we are calling any other module:

```elixir
iex> Students.count()
31
```

Now save the `Students` module to a file called `students.ex`. Lets compile that file using the `elixirc` command:

```elixir
elixirc students.ex
```

Now in that same directory, if we run the `iex` command to start a REPL, Elixir will automatically pull in the compiled `.beam` file into the environment and we can use our `Students` module directly:

```sh
$ iex
iex> Students.count()
31
```

![](/assets/learning_elixir/compile.png)

We'll write most of our code inside modules.
