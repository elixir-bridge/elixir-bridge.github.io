---
layout: post
title: Create a Phoenix App
date: 2016-08-21 12:28:28 -0700
---

### Step 1: Change to your home directory

#### Mac or Linux
Type this in the terminal:
```
cd ~
```

`cd ~` sets our home directory to our current directory.

### Step 2: Create an Elixirbridge directory

To keep things organized, we'll want all of the elixirbridge files in their own directory. Type this in the terminal:
```
mkdir elixirbridge
```
`mkdir` stands for make directory (folder).

We've made a folder called elixirbridge.

### Step 3:
Change to your new elixirbridge directory
Type this in the terminal:
```
cd elixirbridge
```
### Step 4: Create a new Phoenix app
Type this in the terminal:

```
mix phoenix.new test_app
```

The command's output is a list of the files it creates, which will be fairly long. We'll go into detail about what these files are later. Then it will as you to fetch and install dependencies, type `Y` to do this. If there's an error at this point, grab a volunteer to help you.

Change into the project directory:

```
cd test_app
```

Now type this into the terminal:

```
which node
```

You should see something like this in your terminal:

```
/usr/local/bin/npm
```

If you do see this, move on to the next step.
Otherwise type the following into your terminal:

```
brew install node
```

Step 5: Get Dependencies

Type the following into your terminal:

```
mix deps.get
`

Step 6: Install nm and node

```
npm install && node node_modules/brunch/bin/brunch build
```

#### Create the database

Type this in a terminal:
```
mix ecto.create
```

Then, type this in a terminal:
```
mix phoenix.server
```

If phoenix server starts up with no errors, you're golden! It'll look something like this:

```
[info] Running TestApp.Endpoint with Cowboy using http://localhost:4000
21 Aug 13:06:41 - info: compiled 6 files into 2 files, copied 3 in 958ms
```

In your browser, open [localhost:4000](http://localhost:4000). You should see a page Like this:

(TODO: insert screenshot here)
![](/assets/welcome-to-phoenix.png)


#### Step 7 : Generate a database model

Phoenix gives us a phoenix.gen.html task similar to Rails’ rails generate scaffold



If your prompt doesn't already show you that you are in your test_app folder type

```
cd test_app
```

Type this in the terminal:

```

Next lets create a database.

type in

```
$ mix ecto.create
```

You should see something like this -
```
Compiled ...
...
Generated blog.app
The database for Blog.Repo has been created.
```

Now that the database has been created, type this into the terminal:

```
$ mix phoenix.gen.html Drink drinks title:string temperature:string
```

You should see output similar to this:

```
* creating web/controllers/drink_controller.ex
* creating web/templates/drink/edit.html.eex
* creating web/templates/drink/form.html.eex
* creating web/templates/drink/index.html.eex
* creating web/templates/drink/new.html.eex
* creating web/templates/drink/show.html.eex
* creating web/views/drink_view.ex
* creating test/controllers/drink_controller_test.exs
* creating web/models/drink.ex
* creating test/models/drink_test.exs
* creating priv/repo/migrations/20160828191433_create_drink.exs

Add the resource to your browser scope in web/router.ex:

    resources "/drinks", DrinkController

Remember to update your repository by running migrations:

    $ mix ecto.migrate
```

Now let's follow the instructions at the end of that output.

We'll add routes. Open up a file named 'web/router.ex'

Around line 19 (this will vary depending on your editor)

delete the section that looks like

```
 scope "/", TestApp do
    pipe_through :browser # Use the default browser stack

    get "/", PageController, :index

    resources "/pages", PageController
  end
```
and paste in the following

```
scope "/", TestApp do
    pipe_through :browser # Use the default browser stack

    get "/", DrinkController, :index

    resources "/drinks", DrinkController
  end
```


so that section should now look like this

```
scope "/", ElixirBlog do
    pipe_through :browser # Use the default browser stack
    get "/", DrinkController, :index

    resources "/drinks", DrinkController
  end


now type this into the terminal

```
mix ecto.migrate

```
Now lets start start our server up again

Type the following into the terminal

```
$ mix phoenix.server
```

Then go to your browsers and type in
localhost:4000

You should see a page that looks something like this

![test app image](/assets/test-app-index.png)


Wait till your server has loaded like before.

Then in the browser url bar type in:
```
http://localhost:4000/drinks
```

1) Click on new drink

2) Enter Cappuccino for the name

3) Enter 135 for the temperature.

4) Click on "Create Drink".

You should see the following text at the top of the page

![drinks successfully created ](/assets/drinks-created.png)

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

git commit -m "initial commit"

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

```
config :test_app, TestApp.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [host: "example.com", port: 80],
  cache_static_manifest: "priv/static/manifest.json"
```
add

```
secret_key_base: System.get_env("SECRET_KEY_BASE")
```

Now the Section should look like this

```
config :test_app, TestApp.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [host: "example.com", port: 80],
  cache_static_manifest: "priv/static/manifest.json"
  secret_key_base: System.get_env("SECRET_KEY_BASE")
  ```

Don't forget to save the file.


Now we will add the production database configuration to our 'config/prod.exs' file

Open the file.

Paste the following

```
# Configure your database
config :hello_phoenix, HelloPhoenix.Repo,
  adapter: Ecto.Adapters.Postgres,
  url: System.get_env("DATABASE_URL"),
  pool_size: String.to_integer(System.get_env("POOL_SIZE") || "10"),
  ssl: true

right under this section

```
config :test_app, TestApp.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [host: "example.com", port: 80],
  cache_static_manifest: "priv/static/manifest.json"
  secret_key_base: System.get_env("SECRET_KEY_BASE")

```

The top of the 'config/prod.exs' file should now look like

```
config :test_app, TestApp.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [host: "example.com", port: 80],
  cache_static_manifest: "priv/static/manifest.json"
  secret_key_base: System.get_env("SECRET_KEY_BASE")


# Configure your database
config :hello_phoenix, HelloPhoenix.Repo,
  adapter: Ecto.Adapters.Postgres,
  url: System.get_env("DATABASE_URL"),
  pool_size: String.to_integer(System.get_env("POOL_SIZE") || "10"),
  ssl: true
  ```

Next Find the line in the `prod.exs` file that says the following

```
url: [host: "example.com", port: 80],
```
(It should be in the first section of this file we changed).

Replace that line with the following two lines

```url: [scheme: "https", host: "name-of-your-app.herokuapp.com", port: 443],
force_ssl: [rewrite_on: [:x_forwarded_proto]],```

Make sure that you replace the part of the host url that says `name-of-your-app` with the app name that you copied and saved from an earlier step.


Since our configuration is now handling Heroku's environement variables, we can delete the following line from `prod.exs':

```
import_config "prod.secret.exs"
```

Our config/prod.exs should now look like this -

The last thing we need to do is decrease teh timeout for websocket Transport.

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

end

Open the Procfile in your text editor and paste in the following:

```
web: MIX_ENV=prod mix phoenix.server
```

Next go to your app on heroku

[https://dashboard.heroku.com/apps](https://dashboard.heroku.com/apps)

Click on your app

Click on Find Add-ons

In the search bar type

Heroky Postresql

Select the `Heroku Postgres :: Database`
option

Click Provision

Next: go back to your terminal

Type the following in your terminal:

```
Expected Result:

```
Creating heroku-postgresql:hobby-dev on ⬢ stormy-stream-65433... free
Created postgresql-convex-53624 as HEROKU_POSTGRESQL_NAVY_URL
Database has been created and is available
 ! This database is empty. If upgrading, you can transfer
 ! data from another database with pg:copy
Use heroku addons:docs heroku-postgresql to view documentation
```
Next we want to update the number of available connections. The Heroku hobby-dev database allows for 20 connectiosn so we want our number to be slightly lower to account for migrations and mix tasks.


Type the following in your terminal:

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
xvafzY4y01jYuzLm3ecJqo008dVnU3CN4f+MamNd1Zue4pXvfvUjbiXT8akaIF53
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

### Depploy Time!!!

Let's commit all our changes. Copy each of the lines below into your terminal one at a time. Do not do this all at once.

```
$ git add config/prod.exs
$ git add Procfile
$ git add web/channels/user_socket.ex
$ git commit -m "Use production config from Heroku ENV variables and decrease socket timeout"
```

And now DEPLOY!!

Type this into your terminal:

```
$ git push heroku master
```


TODO
explain mix
explain ecto

