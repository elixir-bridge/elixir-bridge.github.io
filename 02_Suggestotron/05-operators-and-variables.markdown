---
layout: page
title: Operators and Variables
date: 2016-10-1 13:38:30 -0700
---

# Operators

Elixir has a lot of built-in operators. We've already seen a few, such as addition (`+`), division (`/`), and `++`/`--` (list manipulation):

```elixir
iex> [1, 2, 3] ++ [4, 5, 6] # [1, 2, 3, 4, 5, 6]
iex> [1, 2, 3] -- [2] # [1, 3]
iex> "Hello" <> "World" # HelloWorld
```

We can also check for boolean operators, such as using `and`, `or`, and `not`. We need to use a boolean as the first argument of these operators. For instance:

```elixir
iex> true and true # true
iex> false or is_atom(:example) # true
```

The `or` and `and` operators are called _short-circut_ operators as they execute the left-side first and if it is enough, the right-hand side will not be executed.

```elixir
iex> false and raise("Error") # false
iex> true or raise("Error")
```

We can use the `||`, `&&`, and `!` operators which accept arguments of all types. All values from these operators evaluate to true except for `false` and `nil`.

```elixir
iex> 1 || true # 1
iex> nil && 13 # nil
iex> !1 # false
```

We can check equality using the `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<`, and `>` comparison operators. The `==` operator and `===` have different levels of strict-ness, where the `==` operator is less restrictive:

```elixir
iex> 1 == 1.0 # true
iex> 1 === 1.0 # false
```

## Variables

In Elixir, we'll use variables all over the place. In Elixir, we can create variables simply by setting the _name_ of a variable equal to it's value using the `=` operator:

```elixir
iex> a = 1 # 1
iex> list = [1, 2, 3]
iex> tuple = {:ok, "Hello"}
```
