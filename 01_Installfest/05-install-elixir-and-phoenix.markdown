---
layout: post
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


Next Step:

[Create an SSH key](06-create-an-ssh-key.html)

Go Back:

[Install and Configure Git](04-install-and-configure-git.html)
