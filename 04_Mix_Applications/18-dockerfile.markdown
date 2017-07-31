## Dockerfile

We are going to use docker to deploy our application. To do so we need to create a dockerfile

Step 1: Dockerfile
Make sure you are in your root app directory and type the following into the commad line. 

```bash
touch dockerfile
```

The dockerfile will specify all of the commands we needed to build a docker image

Step 2: Connect your shell to your maching

Run the following in your terminal:

```bash
eval $(docker-machine env elixir-experiment)
```

This will connect your shell to your machine. 

Copy and paste the following into your dockerfile:

```bash
FROM elixir:1.4.2
ENV PORT=4000 MIX_ENV=prod

ENV APP_NAME=myapp APP_VERSION="0.1.0"

RUN mix local.hex --force && \
    mix local.rebar --force && \
    mkdir /build

WORKDIR /build
COPY ./mix.exs /build
COPY ./mix.lock /build
COPY ./config /build/config
RUN mix do deps.get, deps.compile

COPY . /build
RUN mix do compile, release --verbose
# ADD _build/prod/rel/$APP_NAME .

RUN ln -s /build/_build/prod/rel/$APP_NAME /$APP_NAME

EXPOSE $PORT

WORKDIR /$APP_NAME
CMD trap exit TERM; /$APP_NAME/bin/$APP_NAME foreground & wait
```
