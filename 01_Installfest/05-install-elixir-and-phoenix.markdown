---
layout: page
title: Install Elixir and Phoenix
date: 2016-09-24 12:28:28 -0700
---


### Step 6: Install Elixir

You can either install elixir with asdf or brew. We recommend asdf, but either approach will be sufficient.

### asdf

For asdf follow the setup insructions here - [https://github.com/asdf-vm/asdf](https://github.com/asdf-vm/asdf)

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

Navigate to [https://chocolatey.org/install](https://chocolatey.org/install). 

Install the chocolatey package. 

Then install elixir. Follow the instructions here: [https://chocolatey.org/packages/Elixir](https://chocolatey.org/packages/Elixir)

#### Check Your Installation

To check that Elixir is installed correctly:

`elixir -v`

You should see a version number greater than 1.5, like this:

`Elixir 1.5.1`

Anything above 1.5 is fine.

### Step 7: Install Hex

Type this in the terminal:

```
mix local.hex
```

### Step 8: Install Phoenix

Type this in the terminal:

```
mix archive.install https://github.com/phoenixframework/archives/raw/master/phx_new.ez
```

You will see:

```
Are you sure you want to install archive "https://github.com/phoenixframework/archives/raw/master/phx_new.ez"? [Yn]
```

Answer "Y" to install. Then you should see:

```
* creating /Users/{your user name}/.mix/archives/phx_new
```

#### Verify
Type this in the terminal:
```
mix help | grep phx
```

Expected Result:

```
mix phx.new       # Creates a new Phoenix v1.3.0 application
```

You will likely see other mix commands, but that's the important one.

### Step 9: install Docker
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

run `docker-machine create --driver virtualbox elixir-experiment`


This will create a local image named `elixir-experiment` using virtualbox as the driver. To see your local config:

```
docker-machine env elixir-experiment
```

This command shows the docker environment variables for the environment specified, in this case the environment variables are being set for our local machine named `elixir-experiment`.  Now let's set them up as convenient variables:

```
eval $(docker-machine env elixir-experiment)
```

Double check to make sure that our `$DOCKER_HOST` is pointing to our local machine.

`echo $DOCKER_HOST`

This should reference our local machine. You should see something like the following

`tcp://192.xxxxx`

 We will use this local image to build our elixir app tomorrow.
