---
layout: post
title: Install and Configure git
date: 2016-09-24 12:28:28 -0700
---


### Step 5: Install Git

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


### Step 6: Configure git
Type this in the terminal:

```
git config --global user.name "Your Actual Name"
git config --global user.email "Your Actual Email"
```

#### Verify

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

Next Step:

[Install Elixir and Phoenix](05-install-elixir-and-phoenix.html)

Go Back:

[Set up Operating system](03-macintosh-osx-setup.html)
