---
layout: page
title: Recursion
date: 2016-10-1 13:38:30 -0700
---

## Recursion

We can use the concept of guards with pattern matching to implement somewhat complex functions as simple ones. For instance, let's say we have a function where we want to implement the [Fibonacci](https://en.wikipedia.org/wiki/Fibonacci_number) sequence in elixir. The simplest way for handling fibonacci functions is to use recusion, for instance:

```elixir
defmodule Math do
  def fibonacci(x) when x <= 1, do: x
  def fibonacci(x), do: fibonacci(x - 1) + fibonacci(x - 2)
end
```

Although this might look complex from the outset, it's a fairly succinct method for defining such a complex algorithm.

Erlang (and elixir) implement recursive functions efficiently, so we can rely on recursive statements as a safe, fast method for dealing with recursive functions.

## Pipe operator

One operator that we'll see often is the pipe operator `|>`. The `|>` pipe operator looks scary but really just passes the result of one function on to the next function. Conceptually, it's like running the function:

```
f(d(b(:atom)))
```

The equivalent version using pipes is

```
b(:atom) |> d() |> f()
```

The `pipe` operator helps our code stay clean and readable. We'll use it for cases where we want to transform a request type.
