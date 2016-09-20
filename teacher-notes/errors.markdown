# Installation errors

Here are some of the installation errors we have seen and what to do about them.

## Homebrew

### Could not find i18n-0.7.0 in any of the sources

    % ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    Could not find i18n-0.7.0 in any of the sources
    Run `bundle install` to install missing gems.

Switching to system Ruby from a newer Ruby fixed this:

    rvm use system

### It appears Homebrew is already installed.

    % ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    It appears Homebrew is already installed. If your intent is to reinstall you
    should do the following before running this installer again:
        ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
    The current contents of /usr/local are bin Cellar CODEOFCONDUCT.md etc Frameworks include lib Library LICENSE.txt opt README.md sbin share ssl var .git .github .gitignore

You're all set. Move on to the next step.

### Error: Brunch 2+ requires node.js v4 or higher

      npm install && node node_modules/brunch/bin/brunch build
    Error: Brunch 2+ requires node.js v4 or higher (you have v0.12.7) Upgrade node or use older brunch for old node.js: npm i -g brunch@1

Fix by upgrading node:

    brew ugrade node



