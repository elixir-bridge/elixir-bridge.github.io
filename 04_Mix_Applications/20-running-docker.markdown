## Running Docker

Now that are configuration is set up. Run the following from your command line:

```bash
docker run --rm -it -p 4000:4000 auser/elix /bin/bash
```

It may take a few minutes to build. 

You should see something like the following as output at the end:
```bash
==> Release successfully built!
    You can run it in one of the following ways:
      Interactive: _build/prod/rel/myapp/bin/myapp console
      Foreground: _build/prod/rel/myapp/bin/myapp foreground
      Daemon: _build/prod/rel/myapp/bin/myapp start
 ---> f16c41620360
Removing intermediate container 4029e34ff778
Step 12/15 : RUN ln -s /build/_build/prod/rel/$APP_NAME /$APP_NAME
 ---> Running in 0ce74f1e46e0
 ---> 9fc0c9599a59
Removing intermediate container 0ce74f1e46e0
Step 13/15 : EXPOSE $PORT
 ---> Running in dd7be6652f81
 ---> 65c4e748b19b
Removing intermediate container dd7be6652f81
Step 14/15 : WORKDIR /$APP_NAME
 ---> ee4c010362ea
Removing intermediate container b56275fedbbe
Step 15/15 : CMD trap exit TERM; /$APP_NAME/bin/$APP_NAME foreground & wait
 ---> Running in 1d559d929603
 ---> 5736329bf51b
Removing intermediate container 1d559d929603
Successfully built 5736329bf51b
Successfully tagged auser/elix:latest
```

Then run:

```bash
$ docker run --rm -it -p 4000:4000 auser/elix /bin/bash
```

You will see the following output:

```bash
root@36a75b685457:/build/_build/prod/rel/myapp# 
```

Hit `Ctl D` do exit.

## Find docker-machine ip

Type the following into your command line:

```bash
docker-machine ip elixir-experiment
```

The output should look something like:

```
192.xxx.xxx.xx
```

Now run 
```bash
docker run -p 4000:4000 auser/elix .
```

Then run 

```bash
docker run --rm -it -p 4000:4000 auser/elix /bin/bash
```

Then 

```
docker run -p 4000:4000 auser/elix
```

In your browser go to `your-docker-machine-ip:4000`. 
The web address will look like: `192.xxx.xxx.xxx:4000`

You should see `Not found` printed on the screen.







