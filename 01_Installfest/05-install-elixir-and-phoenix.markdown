---
layout: page
title: Install Elixr and Phoenix
date: 2016-09-24 12:28:28 -0700
---


### Step 6: Install Elixir

#### Homebrew

Before installing anything with homebrew, always update to latest,
by typing this in the terminal:

`brew update`

then you can use homebrew to install elixir:

 `brew install elixir`

#### OR Macports

Alternately, you may install using Macports, by typing this in the terminal:

`sudo port install elixir`

#### Windows installation

Navigate to [http://elixir-lang.org/install.html#windows](http://elixir-lang.org/install.html#windows) and find the web installer. Download it and accept the defaults. This will take a little bit of time as it needs to download the installation files.

#### Check Your Installation

To check that Elixir is installed correctly:

`elixir -v`

You should see:

`Elixir 1.4.2`

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

run the following commands (each might take a little while since they will download and install things):

```
brew tap caskroom/cask
brew cask install virtualbox
brew install docker-machine
```

> *Windows installation* Follow the instructions on [https://docs.docker.com/docker-for-windows/](https://docs.docker.com/docker-for-windows/). 

If that is successful run

`brew install docker`

Docker-machine makes building docker environments in multiple platforms simple. In this case, we'll be building against the google cloud engine, but we can just as easily build our environment with aws, virtualbox, or any other cloud provider supported by docker-machine.

run `docker-machine create --driver virtualbox default`


This will create a local image named `default` using virtualbox as the driver. To see your local config:

```
docker-machine env default
```

This command shows the docker environment variables for the environment specified, in this case the environment variables are being set for our local machine named `default`.  Now let's set them up as convenient variables:

```
eval $(docker-machine env default)
```

Double check to make sure that our `$DOCKER_HOST` is pointing to our local machine.

`echo $DOCKER_HOST`

This should reference our local machine. You should see something like the following

`tcp://192.xxxxx`

 We will use this local image to build our elixir app tomorrow.
