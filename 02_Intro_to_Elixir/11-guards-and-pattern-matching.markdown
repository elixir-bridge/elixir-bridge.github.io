---
layout: page
title: Guards and Pattern Matching
date: 2016-10-1 13:38:30 -0700
---

### Guards and pattern matching

We've looked at pattern matching with elixir earlier. We can use pattern matching with our functions as well. For instance, let's say we want to write a function that checks to see if a number is zero or not.

We _always_ will return true when the number passed in through a function is 0, so we can write our function like so:

```elixir
defmodule Math do
  def zero?(0) do
    true
  end
end
```

Alternatively, more succinctly, we can write this function in the list format to make it smaller:

```elixir
defmodule Math do
  def zero?(0), do: true
end
```

If we run this function in our REPL, we'll see that we can call the `Math.zero?(0)` without errors. However, if we run this with any other number, it will explode with an error.

![](/assets/learning_elixir/zero-matching.png)

It explodes with an error because elixir cannot find a function to run that matches the case where the argument is non-zero. We can write this function by defining a function version with an argument:

```elixir
defmodule Math do
  def zero?(0), do: true
  def zero?(_) do
    false
  end
  # or, the one line version
  # def zero?(_), do: false
end
```

Now if we run the function in our terminal with either 0 or a non-zero number, we can see it does not explode, but instead returns a boolean value of false.

![](/assets/learning_elixir/zero-matching-1.png)

What happens if our requirements change and we want to _also_ say that the string "zero" is equal to zero? We might have to change our function to be more complex, right?

Not necessarily, we can use the concept of _guards_ to add additional functionality to the pattern matching provided by default through Elixir. A _guard_ comes right after the function definition. For instance, to implement our previous function with a guard to match if the argument is a string of "zero", we can add the guard like so:

```elixir
defmodule Math do
  def zero?(0), do: true
  def zero?(x) when x == "zero" do
    true
  end

  def zero?(_), do: false
end
```

Running this in the console and we'll see that we get `true` when we pass in the string of `"zero"`.
