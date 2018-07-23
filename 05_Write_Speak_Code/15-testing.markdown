---
layout: page
title: Testing
date: 2016-10-1 13:38:30 -0700
---

## Testing

Elixir makes testing really Easy. `ExUnit` is built into to every mix app.

Let's run `mix test` in our app and see what we get.

```bash
$ mix test
===> Compiling ranch
===> Compiling cowlib
===> Compiling cowboy
==> mime
Compiling 1 file (.ex)
Generated mime app
==> plug
Compiling 1 file (.erl)
Compiling 48 files (.ex)
Generated plug app
==> my_app
Compiling 1 file (.ex)
Generated my_app app
..

Finished in 0.03 seconds
1 doctest, 1 test, 0 failures

Randomized with seed 440159
```

This command will compile our application and will then run all of our tests.

If we open up the `test` directory in our application, we can see that ExUnit has generated a smoke test for us, to ensure that our tests are running properly.


