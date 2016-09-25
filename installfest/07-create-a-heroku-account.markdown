---
layout: post
title: Creat a Heroku Account
date: 2016-09-24 12:28:28 -0700
---

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


Next Step

[Create Phoenix App](installfest/08-create-phoenix-app.html)


Go Back:

[Creat an SSH key] (installfest/06-create-an-ssh-key.html)

