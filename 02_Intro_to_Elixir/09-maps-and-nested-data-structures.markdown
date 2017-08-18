---
layout: page
title: Maps and Nested Data Structures
date: 2016-10-1 13:38:30 -0700
---


# Maps

Maps in Elixir provide a quick key-value data store. Maps can be created by using the `%{}` syntax:

```elixir
iex> map = %{:a => 1, 2 => :b}
%{2 => :b, :a => 1}
iex> map[:a]
1
iex> map[2]
:b
iex> map[:c]
nil
```

We can use the `.` syntax to access a specific key in the map:

```elixir
iex> map.a
1
```

But not for an element that doesn't exist...

```elixir
iex> map.c
** (KeyError) key :c not found in: %{2 => :b, :a => 1}
```

In comparison to keyword lists, maps do not follow any ordering and allow any value to be set as a key. However, it's recommended to stick to literals such as strings, atoms, and numbers.

## Nested data structures

Elixir provides a way for us to hold variables inside of maps. We'll use this a lot in the Phoenix framework, where we'll have variables that represent data structures in our database. 

For example, we can create a list of users that is a key-value map to another nested map:

```elixir
iex> users = [
  john: %{name: "John", age: 27, languages: ["Erlang", "Ruby", "Elixir"]},
  mary: %{name: "Mary", age: 29, languages: ["Elixir", "F#", "Clojure"]}
]
```

We can then get variables using `[]` (dynamic access) and `.` (strict access) syntax:

```elixir
iex> users[:john].age
27
```

We can then manipulate variables by using the `put_in/2` function to create a new value:

```elixir
iex> users = put_in users[:john].age, 31
iex> users
[john: %{age: 31, languages: ["Erlang", "Ruby", "Elixir"], name: "John"},
 mary: %{age: 29, languages: ["Elixir", "F#", "Clojure"], name: "Mary"}]
```

Check out the [Kernel module documentation](https://hexdocs.pm/elixir/Kernel.html) for other available functions when using nested data structures.

## Executing scripts

So far we've used IEx to execute Elixir code in real-time which is convenient for small, one-line expressions. Rather than typing in the REPL, we can write our Elixir code to a file and execute it as a script using the `elixir` command:

```sh
$ echo "IO.puts \"Hello world\"" > test.exs
$ elixir test.exs
Hello world
```
