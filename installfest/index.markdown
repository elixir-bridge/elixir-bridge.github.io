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
#### Step 4: Install Postgres

Type this in the terminal:
```
brew install postgresql
```


If this is your first time installing Postgres with Homebrew, you'll need to create a database.

Type this into the terminal:

```
initdb /usr/local/var/postgres -E utf8
```

Now you will need to create a user for your Database

Type the following into the terminal:

```
createuser -s postgres
```

Next type this into the terminal:

```
$ launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist

```




#### Step 5: Install Git

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

#### Step 6: Install Elixir

##### Homebrew

Update your homebrew to latest:

Type this in the terminal:

`brew update`

 `brew install elixir`

##### Macports

Type this in the terminal:

`sudo port install elixir`


##### Step :7 Install Hex

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

### Step :9 Configure Git

Type this in the terminal:

```
git config --global user.name "Your Actual Name"
git config --global user.email "Your Actual Email"
```

##### Verify

Type this in the terminal:

```
git config --get user.name
```

Expected Result:
```
your name
```

Type this in the terminal:

```
git config --get user.email
```

Expected Result

```
your email address
```

If on a mac, type this into the terminal

```
git config --global color.ui auto
```

#### Create an SSH Key

An SSH key uniquely identifies you (and your computer) when your computer is communicating with other computers. Think of an SSH key as a type of password.


Step 1:

Let's see if you have a pre-exisiting SSH key on your computer

Type this in the terminal:

```
ls ~/.ssh/id_rsa
```
If you see ** No such file or directory ** you don't have one.

Go on to Generate an SSH key



Otherwise go on to Create a Heroku Account


Step 2: Generate an SSH Key

**
Use the same email address for heroku, git, github, and ssh.**

Type this in the terminal:
ssh-keygen -C your_email@example.com -t rsa


Press enter to accept the default key save location.

Next you'll be asked for a passphrase

option 1: No passphrase
Hit enter to accept blank passphrase, then hit enter again.

option 2: Passphrase
If your computer is shared with other people, as in a work laptop, you should choose and enter a real passphrase. Twice.

After the key generation is complete- your output should look like this -

```
Expected result:
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/student/.ssh/id_rsa):
Created directory '/Users/student/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/student/.ssh/id_rsa.
Your public key has been saved in /Users/student/.ssh/id_rsa.pub.
The key fingerprint is:
88:54:ab:77:fe:5c:c3:7s:14:37:28:8c:1d:ef:2a:8d student@example.com
```
##### Verify

Your brand-new public key is now stored at ~/.ssh/id_rsa.pub

###### Public vs. Private Keys

If you look inside ~/.ssh/, you will notice two files with the same name: id_rsa and id_rsa.pub.

id_rsa.pub is your **public key** and can be shared freely.

id_rsa is your **private key** and must be kept secret.

Add your generated public key to the authentication agent using the following command:

Type this in the terminal:

```
ssh-add ~/.ssh/id_rsa
```

Expected Result

```
Enter passphrase for /Users/student/.ssh/id_rsa:
Identity added: /Users/student/.ssh/id_rsa (/Users/student/.ssh/id_rsa)"
```

Could not open a connection to your authentication agent

If the ssh-agent is not running, you will come across this error. Here are a few commands that you can try to use to start the ssh-agent:

For some Windows machines:
```
eval `ssh-agent -s`
```

For others (confirmed on some Windows 7, 8, 8.1, and 10 setups):

```
eval $(ssh-agent)
```

For Linux:

```
eval `ssh-agent`
```

For additional options, this [StackOverflow thread](http://stackoverflow.com/questions/17846529/could-not-open-a-connection-to-your-authentication-agent) has been helpful:

### Create a Heroku Account

#### Step 1: Visit the Heroku web site

(http://heroku.com)[http://heroku.com]

#### Step 2: Create an Account

Click the big **Sign Up** button

Enter your email address:

#### Step 3: Activate your account

Heroku will send you an activation email. Open it and click on the activation link. It will take you to the Heroku site. Enter and confirm your password. Hit Save.

#### Step 4: Install the Heroku toolbelt

Visit [https://toolbelt.heroku.com/]( https://toolbelt.heroku.com/) clickk the downloand link, and install

##### Verify

Type this in the terminal:

```
heroku version
```

Approximate expected result:

```
heroku-toolbelt/3.30.6 (x86_64-darwin10.8.0) ruby/1.9.3
You have no installed plugins.
```

* Windows users, if heroku version doesn't work, open a new terminal window after the heroku installer has finished.

#### Step 5: Add your SSH key to your Heroku account

Type this in the terminal:

```
heroku keys:add
```

Enter your Heroku email and password, if prompted, and accept the defaults.

#### Step 6: Optional (Create a Github Account)

You can use GitHub to store your code online and access it from anywhere. This step isn't necessary to deploy your apps to the web though.

#### Step 1: Visit the GitHub web site

https://github.com

#### Step 2: Create an Account

Click the green Sign Up for GitHub button (it's about halfway down the page)

Enter a username, your email address and a password.


Use the same email address for heroku, git, github, and ssh. Be sure to use an email account you can log into immediately.

#### Step 3: Select a plan
GitHub provides several levels of account plans but you can create unlimited public repositories with a free plan so for now, you can select that one. Hit Finish sign up.

#### Step 4: Set up SSH authentication with GitHub

Adding an SSH key to GitHub allows you to pull and push data without typing in your password all the time. First we'll copy the key we generated in the Create an SSH Key step and add it to your GitHub account. We'll use a terminal command to do that, so that we don't add any newlines or whitespace that could cause an error.

##### Mac users

Type this in the terminal:

```
pbcopy < ~/.ssh/id_rsa.pub

```

##### Linux users

Type this in the terminal:

```
sudo apt-get install xclip
xclip -sel clip < ~/.ssh/id_rsa.pub
``

sudo apt-get install xclip installs a tiny application, xclip, that lets us copy the contents of a file without opening it. Mac and Windows users have similar things already installed (pbcopy and clip).

##### Windows users

Type this in the terminal:

```
clip < "%userprofile%\.ssh\id_rsa.pub"
```

Now that you have copied the key to your clipboard, you can add it to the GitHub account you created earlier.

##### Add your SSH key to GitHub
Navigate to github.com and make sure you are logged in. On any page on the GitHub site, click your profile photo in the top right corner to the right of the plus sign. In the dropdown menu, click **Settings** to go to the account settings page.

On the account settings page, select **SSH and GPG keys** from the column on the left.

At the top right of this page, click the button that says **New SSH key**. In the title field, give a name for your SSH key, you might call it **My PC** or **Personal MacBook**. In the key field, paste the key you copied.

Click **Add SSH key**

Confirm the action by providing your GitHub Password

#### Step 5: Confirm SSH Authentication

Confirm that you have successfully set up SSH Authentication for GitHub

Windows users cannot perform this step.

Type this in the terminal:

```
ssh -T git@github.com
```
Expected Result:

```
The authenticity of host 'github.com (207.97.227.239)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?
```
You might see a message like this to confirm your key, if it's your correct key continue connecting by typing yes

Expected Result:

Hi username! You've successfully authenticated, but GitHub does not
provide shell access.









