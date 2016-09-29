---
layout: post
title: Deploy a Phoenix App
date: 2016-09-24 12:28:28 -0700
---

#### Deploy A Phoenix App

If your prompt doesn't already show that you are (still) in the test_app folder

Type this in the terminal:

```
cd test_app
```

Type this in the terminal:

```
git init

```

Expected result:

Initialized empty Git repository in c:/Sites/elixirbridge/test_app/.git/

Type this in the terminal:

```
git add -A
```

With Git, there are usually many ways to do very similar things.

*git add foo.txt adds a file named foo.txt
*git add . ("git add dot") adds all new files and changed files, but keeps files that you've deleted
*git add -A adds everything, including deletions

"Adding deletions" may sound weird, but if you think of a version control system as keeping track of changes, it might make more sense.

Type this in the terminal:

```
git commit -m "initial commit"
```

Expected result:

```
a lot of lines like create mode 100644
```

Type this into the terminal:

```
git log
```

Expected Result:

(Your git name and "initial commit" message.)

##### Step 2: Deploy your app to Heroku

##### Step 2.1 Create a Heroku application from this local Phoenix Application

The very first time you use heroku you must enter your Heroku email address and password. Your password may not be shown as you type it, but don't worry, it's being entered! If you have already provided your credentials before, you won't be prompted for them again.


Type this into the terminal:

```
 heroku create --buildpack "https://github.com/HashNuke/heroku-buildpack-elixir.git"
 ```

 Expected Result:
 Something similar to the following -

```
Creating app... done, ⬢ stormy-stream-65433
Setting buildpack to https://github.com/HashNuke/heroku-buildpack-elixir.git... done
https://stormy-stream-65433.herokuapp.com/ | https://git.heroku.com/stormy-stream-65433.git
```

Copy and paste the name of your app somewhere, you will need it for a later step. The the name of our app is listed in the terminal right under the line `Creating app... done,`

In this case..the name of the app is `stormy-stream-65433`

--buildpack option we are passing allows us to specify the Elixir buildpack we want Heroku to use.

A buildpack is a convenient way of packaging framework and/or runtime support. In our case it's installing Erlang, Elixir, fetching our application dependencies, and so on, before we run it.

Now Type this into the terminal:

```
heroku buildpacks:add https://github.com/gjaldon/heroku-buildpack-phoenix-static.git
```

Expected output:

```
Buildpack added. Next release on stormy-stream-65433 will use:
  1. https://github.com/HashNuke/heroku-buildpack-elixir.git
  2. https://github.com/gjaldon/heroku-buildpack-phoenix-static.git
Run git push heroku master to create a new release using these buildpacks.
```
This buildpack allows us to compile static assets for Phoenix deployment.

##### Setting Enviroment Variables

Every new project comes with a config file, `config/prod.secret.exs` which stores configuration that shold not be committed with source code.

Phoenix adds it to the .gitingnore file by default.

The Problem is Heroku uses environment variables to pass sensitive information to our application.

##### Setup config files for Deploy

Open `config/prod.exs`

 At the bottom of this section

 delete the contents of that file.

 Then paste in the following

```
use Mix.Config

config :test_app, TestApp.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [scheme: "https", host: "your-app-name.herokuapp.com", port: 443],
  force_ssl: [rewrite_on: [:x_forwarded_proto]],
  cache_static_manifest: "priv/static/manifest.json",
  secret_key_base: System.get_env("SECRET_KEY_BASE")

# Do not print debug messages in production
config :logger, level: :info
```

Make sure that you change the following line to include the name of your app

```
url: [scheme: "https", host: "your-app-name.herokuapp.com", port: 443]
```

Don't forget to save the file.



Now we will add the production database configuration to our 'config/prod.exs' file

Open the file.

Paste the following at the bottom of the file.

```
# Configure your database
config :test_app, TestApp.Repo,
  adapter: Ecto.Adapters.Postgres,
  url: System.get_env("DATABASE_URL"),
  pool_size: String.to_integer(System.get_env("POOL_SIZE") || "10"),
  ssl: true
```

The top of the 'config/prod.exs' file should now look like --

```
use Mix.Config

config :test_app, TestApp.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [scheme: "https", host: "stormy-stream-65433.herokuapp.com", port: 443],
  force_ssl: [rewrite_on: [:x_forwarded_proto]],
  cache_static_manifest: "priv/static/manifest.json",
  secret_key_base: System.get_env("SECRET_KEY_BASE")

# Do not print debug messages in production
config :logger, level: :info


# Configure your database
config :test_app, TestApp.Repo,
  adapter: Ecto.Adapters.Postgres,
  hostname: System.get_env("NEW_DATABASE_URL"),
  pool_size: String.to_integer(System.get_env("POOL_SIZE") || "10"),
  ssl: true,
  database: System.get_env("DATABASE"),
  username: System.get_env("USERNAME"),
  password: System.get_env("PASSWORD")
```

Next Find the line in the `prod.exs` file that says the following

```
url: [host: "example.com", port: 80]
```
(It should be in the first section of this file we changed).

Replace that line with the following two lines

```
url: [scheme: "https", host: "name-of-your-app.herokuapp.com", port: 443],
```

Make sure that you replace the part of the host url that says `name-of-your-app` with the app name that you copied and saved from an earlier step.

```
use Mix.Config

config :test_app, TestApp.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [scheme: "https", host: "stormy-stream-65433.herokuapp.com", port: 443],
  force_ssl: [rewrite_on: [:x_forwarded_proto]],
  cache_static_manifest: "priv/static/manifest.json",
  secret_key_base: System.get_env("SECRET_KEY_BASE")

# Do not print debug messages in production
config :logger, level: :info


# Configure your database
config :test_app, TestApp.Repo,
  adapter: Ecto.Adapters.Postgres,
  hostname: System.get_env("NEW_DATABASE_URL"),
  pool_size: String.to_integer(System.get_env("POOL_SIZE") || "10"),
  ssl: true,
  database: System.get_env("DATABASE"),
  username: System.get_env("USERNAME"),
  password: System.get_env("PASSWORD")
```

The last thing we need to do is decrease the timeout for websocket Transport.

Open `web/channels/user_socket.ex`

Under '##Transports`

replace the following line

```
transport :websocket, Phoenix.Transports.WebSocket
```
with

```
 transport :websocket, Phoenix.Transports.WebSocket, timeout: 45_000
```

This ensures that any idle connections are closed by Phoenix before they reach Heroku's 55 second timeout window.

#### Create Profile

In your terminal make sure you are in your test_app directory.

Then type:

```
touch Procfile.txt

```

Open the Procfile in your text editor and paste in the following:

```
web: elixir -S mix phoenix.server
```

Next type the following into your terminal (do one line at a time)

```
$ heroku addons:create heroku-postgresql:dev
```

next type the following in your terminal:

```
$ heroku config:set MIX_ENV=prod
```

```
heroku config:set POOL_SIZE=18
```
Expected Result:

```
Setting POOL_SIZE and restarting ⬢ stormy-stream-65433... done, v7
POOL_SIZE: 18
```

When Running a mix task, you want to limit the pool size like so -

```
$ heroku run "POOL_SIZE=2 mix hello_phoenix.task"
```

This is so ecto does not attempt to open more thatn the available connections

##### Create SECRET_KEY_BASE config based on Random string.

Type the following into your terminal:

```
mix phoenix.gen.secret
```
Expected Result:
Something like below, but your string will be different so don't expect the output to be the same.

```
sadshfsldfhdfskdfhasjdhf121223jfjksasdfs
```

Copy the string that is in your terminal.

Now we need to set it in heroku

Type this into your terminal:

```
heroku config:set SECRET_KEY_BASE="your-secret-key-string-from-the-last-step"
```
Expected Result:

```
Setting SECRET_KEY_BASE and restarting ⬢ stormy-stream-65433... done, v8
SECRET_KEY_BASE: your-secret-key
```

If you need to make any of your config variables available at compile time, you will need to explicitly define which ones in a configuration file.
Create a file elixir_buildpack.config in your application's root directory and add a line like: config_vars_to_export=(MY_VAR) [See more](https://github.com/HashNuke/heroku-buildpack-elixir#specifying-config-vars-to-export-at-compile-time)

Next open up your 'Prod.exs file'

There should be a section towards the bottom of the file that looks like this

```
# Configure your database
config :test_app, TestApp.Repo,
  adapter: Ecto.Adapters.Postgres,
  hostname: System.get_env("NEW_DATABASE_URL"),
  pool_size: String.to_integer(System.get_env("POOL_SIZE") || "10"),
  ssl: true,
  database: System.get_env("DATABASE"),
  username: System.get_env("USERNAME"),
  password: System.get_env("PASSWORD")
```

make sure that the name after 'config' is the name of your app,

it should look like this

```
config :your-app-name, YourAppName.repo
```

Next Step:

[Deploy To Heroku](11-deploy-to-heroku.html)

Go Back:

[Generate a database model](09-generate-a-database-model.html)
