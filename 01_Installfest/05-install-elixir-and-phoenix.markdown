---
layout: page
title: Install Elixr and Phoenix
date: 2016-09-24 12:28:28 -0700
---


### Step 6: Install Elixir

#### Homebrew

Update your homebrew to latest:

Type this in the terminal:

`brew update`

 `brew install elixir`

#### Macports

Type this in the terminal:

`sudo port install elixir`


### Step :7 Install Hex

Type this in the terminal:

```
mix local.hex
```

### Step 8: Install Phoenix

Type this in the terminal:

```
mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez
```

You will see:

```
Are you sure you want to install archive "https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez"? [Yn]
```

Answer "Y" to install. Then you should see:

```
* creating /Users/{your user name}/.mix/archives/phoenix_new
```

#### Verify
Type this in the terminal:
```
mix help | grep phoenix
```

Expected Result:
```
mix local.phoenix     # Updates Phoenix locally
mix phoenix.new       # Creates a new Phoenix v1.2.1 application
```


### Step 8 install Docker
If you are not building the elixir app tomorrow you can skip this step.

run `brew install docker-machine`

If that is successful run 

`brew install docker`

Docker-machine makes building docker environments in multiple platforms simple. In this case, we'll be building against the google cloud engine, but we can just as easily build our environment with aws, virtualbox, or any other cloud provider supported by docker-machine. 



run `docker-machine create --driver virtualbox default`


This will create a local image names `default` using virtualbox as the driver

Let's make sure that our `$Docker_HOST` is pointing to our local machine.

`echo $DOCKER_HOST`

This should reference our local machine. You should see something like the following 

`tcp://192.xxxxx`

Then type 

`docker-machine env default`


This will export our environment variables for our local machine

`eval $(docker-machine env default)`

This command sets the docker environment variables for the environment specified, in this case the environment variables are being set for our local machine named `default`
 
 We will use this local image to build our elixir app tomorrow. 
