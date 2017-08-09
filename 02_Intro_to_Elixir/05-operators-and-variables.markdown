---
layout: page
title: Operators and Variables
date: 2016-10-1 13:38:30 -0700
---

# Operators

Elixir has a lot of built-in operators. We've already seen a few, such as addition (`+`), division (`/`), and those for list manipulation (`++` and `--`):

```elixir
iex> [1, 2, 3] ++ [4, 5, 6]
[1, 2, 3, 4, 5, 6]
iex> [1, 2, 3] -- [2]
[1, 3]
iex> "Hello " <> "World"
"Hello World"
```

There are also boolean operators, such as `and`, `or`, and `not`. We need to use a boolean or any function that returns either true or false as the first argument of these operators.

### And

Elixir will evaluate the first term in the expression with the `and` operator. If that term returns true, it will move on to the second term. If it's false, it won't evaluate the second term.

Try the following:

```elixir
iex> true and true
true
iex> is_atom("string") and IO.puts("This won't print")
false
```

### Or

Or is similar, in that it will evaluate the first term, but if it is _true_, it won't evaluate the second term.

Try the following:

```elixir
iex> false or true
true
iex> true or IO.puts("This won't print")
true
```

The `or` and `and` operators are called _short-circut_ operators as they execute the left-side first and only execute the right side if necessary.

We can use the `||` (logical OR), `&&` (logical AND), and `!` (logical not) operators which accept arguments of all types. All values from these operators evaluate to true except for `false` and `nil`.

Try the following:

```elixir
iex> 1 || true
1
iex> nil && 13
nil
iex> !1
false
```

### Equality

We can compare values using the `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<`, and `>` comparison operators. The `==` operator and `===` have different levels of strict-ness, where the `==` operator is less restrictive:

```elixir
iex> 1 == 1.0
true
iex> 1 === 1.0
false
```

## Variables

In Elixir, we'll use variables all over the place. Assigning values to variables in Elixir works differently than it does in imperative languages like Ruby or Javascript. Let's look at an example.

```elixir
iex> x = 2
iex> y = 3
```

If we look at the code, it appears like we have variables on the left-hand side of our expression and values on the right. And thus it may seem that the values on the right are being "assigned" to the values on the left. However in Elixir there is no assignment operator. The `=` is called the match operator. What does this mean?

In Elixir the `=` matches the term on the right to the "pattern" on the left. In our example, the variable will match any data type that Elixir allows, and then the value of that term is bound to the variable. 

```elixir
iex> a = 1
iex> list = [1, 2, 3]
iex> tuple = {:ok, "Hello"}
```

Note that Erlang (and thus Elixir) create immutable data. That is, the original tuple is not replaced, but a new tuple based upon the first one is created.
It turns out that even though it feels like a hinderance, using immutable data makes our software easier to reason about and never need to worry about overwriting variables in memory (thus preventing race conditions) and more.
Although we don't need to focus on this now, it's a good idea to keep in mind that no variable is manipulated after it's created, but that a new one is created.
