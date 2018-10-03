---
layout: page
title: Environments
date: 2016-10-1 13:38:30 -0700
---

## Environments

We will have 3 different environments in our application:

* :dev default environment
* :test test environment
* :prod a production environment

To switch between environments, we can set the `MIX_ENV` environment variable.

`MIX_ENV=prod mix compile`
