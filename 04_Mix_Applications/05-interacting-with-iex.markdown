## Interacting in iex

We can start the app with the command `iex -S mix`: 

```bash
$ iex -S mix
Erlang/OTP 19 [erts-8.3] [source] [64-bit] [smp:8:8] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

===> Compiling ranch
===> Compiling cowlib
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
Interactive Elixir (1.4.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> 
```


## Mix Compile

Next let's run `mix compile`. This will compile all of our dependencies for our application.


