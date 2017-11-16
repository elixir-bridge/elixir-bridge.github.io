## Control structures

We often want to run a check on a particular state of a variable.

### `case`

A very basic case statement:

```elixir
dog = "PUPPY"
> "PUPPY"

case dog do
  "PUPPY" -> "CUTE!!!!!!"
  _ -> "BOOOOOOO"
end
> "CUTE!!!!!!"
```

The `case` function allows us to compare a value against several patterns until we find one that matches. Copy the following into iex:

```elixir
case_statement = fn x ->
  case x do
  {4, 5, 6} ->
      "matches {4,5,6}"
  {1, x, 3} ->
      "This sets x to #{x}"
  _ ->
      "Matches any value not previously matched"
  end
end
```

Now, try calling the function:

```elixir
iex(2)> case_statement.({4,5,6})
"matches {4,5,6}"
iex(3)> case_statement.({1,4,6})
"Matches any value not previously matched"
iex(4)> case_statement.({1,4,3})
"This sets x to 4"
```

We can also use _guards_ to check against extra conditions in a `case` statement. This is useful for setting _extra_ conditions not previously covered in the match statement:

```elixir
case_statement = fn x ->
  case x do
  {1, x, 3} when x > 0 ->
      x
  end
end

case_statement.({1,2,3})
case_statement.({1,-5,3})
```

When there is no match, as in the second call, we get an error:

```elixir
iex(15)> case_statement.({1,-5,3})
** (CaseClauseError) no case clause matching: {1, -5, 3}
```

We can use lots of different operators in the guard clauses above. The documentation at [http://elixir-lang.org/getting-started/case-cond-and-if.html#expressions-in-guard-clauses](http://elixir-lang.org/getting-started/case-cond-and-if.html#expressions-in-guard-clauses) covers all of the operators we have available to us.

### `cond`

The `cond` function allows us to check against the conditions which evaluate to true rather than just different values. It's similar to the `case` statement, but evaluates functions and uses the result to pattern match. Try the following:

```elixir
conditional = fn x ->
  cond do
    2 + x == 5 ->
      "This is not true"
    2 * x == 3 ->
      "This is not true"
    1 + x == 2 ->
      "This does match"
  end
end
conditional.(1)
```

### `if` and `unless`

We can check a single value by using the `if` and `unless`.

```elixir
iex> if true do
       "This is true"
     end
iex> unless true do
      "This won't be seen"
     end
```

We can also use `else` in our `if` and `unless` blocks as well:

```elixir
iex> if false do
        "This won't be seen"
     else
        "This will be seen"
     end
```

### `do/end` blocks

We've seen the `do/end` blocks in our previous operators. They allow us to define the start and end block to be executed if a condition has been met. For instance:

```elixir
iex> if true do
        a = 1 + 2
        a + 10
     end
```

And the equivalent using:

```elixir
iex> if true, do: (
        a = 1 + 2
        a + 10
     )
```
