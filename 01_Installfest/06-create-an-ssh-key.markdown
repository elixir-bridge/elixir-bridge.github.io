---
layout: page
title: Create an SSH Key
date: 2016-09-24 12:28:28 -0700
---


### Step 10: Create an SSH Key

An SSH key uniquely identifies you (and your computer) when your computer is communicating with other computers. Think of an SSH key as a type of password.


#### Step 10.1: Check for an existing key

Let's see if you have a pre-exisiting SSH key on your computer

Type this in the terminal:

```
ls ~/.ssh/id_rsa
```
If you see `No such file or directory` you don't have one.

Continue to Generate an SSH key

Otherwise skip ahead to Create a Heroku Account

#### Step 10.2: Generate an SSH Key

**Use the same email address for Heroku, git, GitHub, and ssh.**

Type this in the terminal:


```
ssh-keygen -C your_email@example.com -t rsa
```

Press enter to accept the default key save location.

Next you'll be asked for a passphrase

##### Option 1: No passphrase
Hit enter to accept blank passphrase, then hit enter again.

##### Option 2: Passphrase
If your computer is shared with other people, as in a work laptop, you should choose and enter a real passphrase. Twice.

After the key generation is complete- your output should look like this -

```text
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

#### Step 10.3: Verify

Your brand-new public key is now stored at ~/.ssh/id_rsa.pub

##### Public vs. Private Keys

If you look inside ~/.ssh/, you will notice two files with the same name: id_rsa and id_rsa.pub.

id_rsa.pub is your **public key** and can be shared freely.

id_rsa is your **private key** and must be kept secret.

Add your generated public key to the authentication agent using the following command:

Type this in the terminal:

```text
ssh-add ~/.ssh/id_rsa
```

Expected Result

```text
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
