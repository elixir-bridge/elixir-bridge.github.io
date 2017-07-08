## Testing

Elixir makes testing really Easy. `ExUnit` is built into to every mix app. 

Let's run `mix test` in our app and see what we get. 

```bash
$ mix test
===> Compiling ranch
===> Compiling cowlib
src/cow_multipart.erl:392: Warning: crypto:rand_bytes/1 is deprecated and will be removed in a future release; use crypto:strong_rand_bytes/1

===> Compiling cowboy
==> mime
Compiling 1 file (.ex)
Generated mime app
==> plug
Compiling 44 files (.ex)
Generated plug app
==> myapp
Compiling 1 file (.ex)
Generated myapp app
..

Finished in 0.03 seconds
2 tests, 0 failures

Randomized with seed 306366
```

This command will compile our application and will then run all of our tests.

If we open up the `test` directory in our application, we can see that ExUnit has generated a smoke test for us, to ensure that our tests are running properly.


