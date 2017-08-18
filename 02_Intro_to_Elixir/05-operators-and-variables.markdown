---
layout: page
title: Operators and Variables
date: 2016-10-1 13:38:30 -0700
---

### Comparison

Let's take a look at how we might compare variables in Elixir

Here are some examples.

 Try typing the examples below into your console

```elixir
1 + 1 == 2
1 > 2
2 <= 4
1 != 2
```

### Strict Comparison

```elixir
2 == 2.0 # true
2 === 2.0 # false
```

What is different about the expression above?
*hint: Thing about data types.

## Variables

In Elixir, we'll use variables all over the place. Assign values to variables in elixir works differently than it does in imperative languages like Ruby or Javascript.

However for now let's pretend that "assignment" works just as it does in other languages.

We will go into what is happening under the hood in the section on Pattern Matching.

```elixir
iex> x = 2
iex> y = 3
```

What values do x and y have now?

All of the following can be variables

```elixir
a = 1
b = 0x0F
c = div(b, a)
```

### How Assignment Actually works in Elixir

```elixir
iex> x = 2
iex> y = 3
```

If we look at the code above. It looks like we have variables on the left-hand side of our expression and values on the right. And it appears that the values on the right are being "assigned" to the values on the left. However in elixir there is no assignment operator. The "=" is called the match operator. What does this mean?

In elixir the "=" matches the term on the right to the "pattern" on left.

```elixir
iex> a = 1 # 1
iex> list = [1, 2, 3]
iex> tuple = {:ok, "Hello"}
```

Note that Erlang (and thus Elixir) create immutable data. That is, the original tuple is not replaced, but a new tuple based upon the first one is created.
It turns out that even though it feels like a hinderance, using immutable data makes our software easier to reason about and never need to worry about overwriting variables in memory (thus preventing race conditions) and more.
Although we don't need to focus on this now, it's a good idea to keep in mind that no variable is manipulated after it's created, but that a new one is created.

# Operators

Elixir has a lot of built-in operators. We've already seen a few, such as addition (`+`), division (`/`), and `++`/`--` (list manipulation):

```elixir
iex> [1, 2, 3] ++ [4, 5, 6] # [1, 2, 3, 4, 5, 6]
iex> [1, 2, 3] -- [2] # [1, 3]
iex> "Hello " <> "World" # "Hello World"
```

There are also boolean operators, such as `and`, `or`, and `not`. We need to use a boolean or any function that returns either true or false as the first argument of these operators.

### And

Elixir will evaluate the first term in the expression with the `and` operator. If that term returns true, it will move on to the second term. If it's false, it won't evaluate the second term.

Type the following:

```elixir
iex> true and true # true
iex> is_atom("string") and IO.puts("This won't print") # false
```

### Or

Or is similar, in that it will evaluate the first term, but if it is _true_, it won't evaluate the second term.

Type the following:

```elixir
iex> false or true #true
iex> true or IO.puts("This won't print") # true
```

The `or` and `and` operators are called _short-circut_ operators as they execute the left-side first and only execute the right side if necessary.

We can use the `||` (logical OR), `&&` (logical AND), and `!` (logical not) operators which accept arguments of all types. All values from these operators evaluate to true except for `false` and `nil`.

Type the following(one line at a time):

```elixir
iex> 1 || true # 1
iex> nil && 13 # nil
iex> !1 # false
```

### Equality

We can compare values using the `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<`, and `>` comparison operators. The `==` operator and `===` have different levels of strict-ness, where the `==` operator is less restrictive:

```elixir
iex> 1 == 1.0 # true
iex> 1 === 1.0 # false
```
