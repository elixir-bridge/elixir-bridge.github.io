---
layout: page
title: Install and Configure git
date: 2016-09-24 12:28:28 -0700
---


### Step 5: Install Git

Next we'll install Git, a popular version control system.

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

### Windows installation

Head to [git-scm.com/download/win](http://git-scm.com/download/win) and download the Windows installer. Run the executable and choose the default options.


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

Expected Result:
```
your email address
```

If on a mac, type this into the terminal

```
git config --global color.ui auto
git config --get color.ui
```

Expected Result:
```
auto
```