---
layout: page
title: Pattern Matching
date: 2016-10-1 13:38:30 -0700
---


## Pattern matching

One of the more powerful ideas in Erlang (and therefore Elixir) is using destructuring and pattern matching. To handle these concepts, Elixir allows us to break up lists by their placement. For instance:

```elixir
iex> [a, b, c] = [1, 2, 3]
iex> a # 1
iex> c # 3
```

We'll also use the head and tail operators to get a list's head and tail elements in a destructured way:

```elixir
iex> [ head | tail] = [1, 2, 3] # [1, 2, 3]
iex> head # 1
iex> tail # [2, 3]
iex> ## We can also preprend values using this destructuring
iex> [1 | [2, 3]] # [1, 2, 3]
```

Lists aren't the only data structure that allows us to pattern match. We can pattern match on tuples as well. For instance:

```elixir
iex> {a, b, c} = {:hello, "world", 42}
iex> a # :hello
iex> c # 42
```

> This works as the tuples are the same size. We'll get a `MatchError` if the size of the tuples are different
>
> ```elixir
> {a, b, c} = {:ok, "hello"} # MatchError
> ```

We'll also use pattern matching to match on specific values of a tuple. This is incredibly useful for checking results of functions, for instance.

```elixir
iex> {:ok, msg} = {:ok, "Hello world"}
iex> msg # "Hello world"
```

If we are only interested in a single value in a pattern, we'll use the `_` notation which is a common way of saying we don't have need for this value in a pattern. For instance, a common usecase is if we want to only get the head of a list.

```elixir
iex> [head | _] = [1, 2, 3]
iex> head # 1
```
