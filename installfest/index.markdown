---
layout: page
title: Installfest
date: 2016-08-15 00:13:42 -0600
---

This is a step by step guide for installing Elixir, Phoenix, and other tools for developing your first application. If you want to contribute, please see our [Contributing Guide](INSERT GUIDE THERE TODO).

### Step 1: Prepare for the Installfest

**You must bring:**

* Your laptop. You need to have a working wifi connection, a browser and an email account you can readily access.
* If you have a choice between a Mac and a Windows laptop, please bring the Mac.
Linux is an acceptable alternative, but the Installfest is only tested on Ubuntu.
*Power cord for your laptop
*If you already have accounts on Heroku or GitHub, make sure you know your username and password.

### Step 2: Don't Panic!

Even if you get stuck, please go through the rest of the instructions and download all the things you'll need. Bandwidth will be at a premium during the workshop, so it will help immensely to have everything on your laptop already.

There are a lot of steps, and the instructions may seem like they're in a foreign language, but: don't panic! By the end of the workshop, you'll know what everything is and how to use it.

### Step 3: Read This Overview

Here's a list of tools you'll be installing. As you go through the workshop, we'll explain what each one is for and how to use it.

* **Elixir.** A programming language
* **Phoenix.** A framework for making web applications with Elixir. It does a lot of the setting up work for you and creates a model-view-controller structure for your web application. We'll go into more detail about that later.
* **Git.** A revision or source control system. It creates a repository, which is a complete history of your programming changes, so you can undo changes and roll back to previous versions of your work if something has gone wrong.
* **GitHub.** (optional)
* **Heroku.** An application server, which hosts your application during development. This allows you to get your application online and interact with it from any browser, instead of just on your local machine.
* **Atom.** To write programs in Elixir, you need a text editor to create, edit and save Elixir files.
* To write programs in Elixir, you need a text editor to create, edit and save Elixir files.


You will also create an account on Heroku, an application hosting platform.

If you already have an account on Heroku, make sure you know your username and password.

If you've already installed the above tools and are confident they are setup correctly, skip ahead to the Get a Sticker step.

Next Step:

Choose your operating system below.

#### Mac

#### Step 1: Learn your Mac OS X Version**

* Click on the Apple icon in the top left of your screen.
* Select "About This Mac"
* In the window that comes up, under the title "Mac OS X" there will be a version number.

If you have 10.9 or above, you're good to go. Otherwise, flag down a volunteer, and they'll help you with the next steps. If you're reading this in advance, now is a good time to [upgrade](http://www.apple.com/osx/how-to-upgrade/).

#### Step 2: Install Xcode Command Line tools

Xcode Command Line Tools include lots of tools your computer needs to set up new software.

## Check to see if you have the tools installed

Type this in the terminal:
```
gcc --version
```

Expected result:

```
Configured with: --prefix=/Library/Developer/CommandLineTools/usr --with-gxx-include-dir=/usr/include/c++/4.2.1
Apple LLVM version 6.0 (clang-600.0.54) (based on LLVM 3.5svn)
Target: x86_64-apple-darwin14.0.0
Thread model: posix
```

If you see something about Darwin and LLVM, you are good to go. If not, use one of the steps below to install the tools. Come back afterwords and run this command to make sure it works!

### If you see something about Darwin and LLVM, you are good to go. If not, use one of the steps below to install the tools. Come back afterwords and run this command to make sure it works!

Option 1: Install XCode Command Line Tools using software update

You can install these tools by trying to run a command that requires them.

#### Step 1.1: Run the xcode-select command

Type this in the terminal:

```
xcode-select --install
```

#### Step 1.2: Install the tools

Click on the "Install" button. When the download finishes, go back and run the test to make sure it works.

#### Option 2: Install Command Line Tools for XCode
Visit the [Apple Developer Downloads Page](https://developer.apple.com/download/)

Download and install the latest **Command Line Tools** for Xcode package for your operating system.This requires you to register for an Apple Developer account.

### Step 2: Install Homebrew

Type this in the terminal:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

You may have to press 'ENTER' when prompted and type in your password.


If that doesn't work, visit [https://github.com/Homebrew/homebrew/wiki/installation](https://github.com/Homebrew/homebrew/wiki/installation) and follow the instructions there.

Check:

Type this in the terminal:

```
brew -v
```

Approximate expected result:

```
Homebrew 0.9.5
```

#### Step 4: Install Git

Next we'll install Git, the most popular version control system in the Ruby world:

Type this in the terminal:

```
git --version
```

Approximate expected result:

```
git version 2.x.x
```

If you have this, move on to the next step.

Otherwise, type this in the terminal:
```
brew install git
```

Check that you have the right version:

Type this in the terminal:

```
git --version
```

Approximate expected result:

```
git version 2.x.x
```

#### Step 5: Install Elixir

##### Homebrew

Update your homebrew to latest:

Type this in the terminal:

`brew update`

 `brew install elixir`

##### Macports

Type this in the terminal:

`sudo port install elixir`


##### Step 6: Install Hex

Type this in the terminal:

```
mix local.hex
```

### Step 7: Install Phoenix

Type this in the terminal:

```
mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez
```

You will see:
```Are you sure you want to install archive "https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez"? [Yn]
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

### Step 8: Install Git

TODO: Configure Git Section

### Step 9: Install Postgres

    brew install postgresql

Open a new Terminal window and launch Postgres:

    postgres -D /usr/local/var/postgres

When you close this window, Postgres will quit.

Now return to your original Terminal window and type:

    createuser --createdb postgres
