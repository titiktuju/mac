This guide covers the basics of setting up a development environment on a new Mac. Whether you are an experienced programmer or not, this guide is intended for everyone to use as a reference for setting up your environment or installing languages/libraries.

# Homebrew
This will allow you to install almost any app from the command line. In previous versions, you’d have to install XCode or Command Line Tools before using this, but that step is no longer necessary.

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Mac App Store
The Mac App Store command line interface, or mas-cli, will allow you to install from the App Store.

```
brew install mas
```

**Sign in**

If you haven’t already logged into the App Store, you can do so now.

```
mas signin email@email.com
```

### Brewfile
Now I’ll create a file called Brewfile in my main directory, which will list all the programs I want on the computer, and install them in a bundle.

Open Terminal, which will be in your home folder by default (/Users/you). Create the file.

```
touch Brewfile
```

You can edit the file with TextEdit, or by typing nano Brewfile. If you choose to edit with nano, you can save the file by typing ```Control + O to save```, and ```Control + X``` to exit the file.

### List of Programs

Here are all the programs I intend to install with a brief description. You can choose to add or subtract any programs you’d like. They’re all free.

1. [Cask](https://caskroom.github.io/) – an extension to Homebrew that will allow you to install almost any program that exists for a Mac
2. [Git](https://git-scm.com/) – for version control
3. [npm](https://www.npmjs.com/) – Node Package Manager (yes, we’re installing package managers with package managers. Welcome to current year! Also, npm doesn’t actually stand for that, but shh.
4. [Firefox](https://www.mozilla.org/en-US/firefox/products/) – a front end dev should have all the major browsers installed
5. [Google Chrome](https://www.google.com/chrome/) – web browser
6. [MAMP](https://www.mamp.info/en/) – simplify and sandbox your development environment, if you choose
7. [Opera](http://www.opera.com/) – web browser
8. [Spectacle](https://www.spectacleapp.com/) – excellent free app for resizing your windows
9. [Sequel Pro](https://www.sequelpro.com/) – excellent free GUI for MySQL databases
10.[VLC Media Player](http://www.videolan.org/vlc/index.html) – it plays everything!

Below are the entire contents of my Brewfile, which will install all the above programs with a single command.

```
tap 'caskroom/cask'

brew 'git'
brew 'npm'
brew 'docker'
brew 'docker-machine'

cask 'chefdk'
cask 'virtualbox'
cask 'vagrant'
cask 'vagrant-manager'
cask 'firefox'
cask 'gimp'
cask 'google-chrome'
cask 'google-hangouts'
cask 'mamp'
cask 'opera'
cask 'spectacle'
cask 'sequel-pro'
cask 'vlc'
```

Now simply run this command to install the bundle.

```
brew bundle install
```

## Bash

### Config – ```~/.bash_profile```
Now that we have all our programs installed and Homebrew all nice and new, we should create a simple script to keep Homebrew up to date. I found this handy command on this Best of Homebrew gist.

First, create a ```.bash_profile``` dotfile in your home folder.

```
touch .bash_profile
```

We’ll create a bash alias to combine all the commands to keep Homebrew clean and up to date.

```
alias brewup='brew update; brew upgrade; brew prune; brew cleanup; brew doctor'
```

Run the following command.

```
source ~/.bash_profile
```

Now you can run brewup to update, upgrade, prune, cleanup, and doctor Homebrew. It’s a good idea to do this often, even daily.

```
brewup
```

## SSH
If you use SSH (Secure Shell) to connect to any remote hosts via the command line, you can simplify the process.

### Generate SSH key
You can [generate an SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) to distribute.

```
ssh-keygen -t rsa -b 4096 -C "email@email.com"
```

### Node.js
We’re going to use Node Version Manager (nvm) to install Node.js.

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
```

Install the latest version.

```
nvm install node
```

Restart terminal and run the final command.

```
nvm use node
```

Confirm that you are using the latest version.

```
node -v
```

You can also test with `which node`, which will output your Node path and version number.

And for later, here’s how to update:

```
nvm install node --reinstall-packages-from=node
```

## Node Package Manager
I have npm installed, and npm is mostly used locally for projects. The only thing I use globally at the moment is Gulp.

### Gulp

Install Gulp globally.

```
npm install --global gulp-cli
```

### Ruby
Ruby is required to run Jekyll, a popular static site generator. I’m going to download Ruby Version Manager (rvm) to make sure I have the updated version of Ruby without messing with the built-in system Ruby.

### Download rvm

```
\curl -sSL https://get.rvm.io | bash -s stable
```

### Install Ruby version
You can look for and install the latest version by number, or by running the below command.

```
rvm install ruby-head
```

You can run `rvm list` to see the full list of versions available. To use the latest version, find the number and run this command.

```
rvm --default use 2.4.0
```

Confirm that you are using the latest version.

```
rvm -v
```

You can also test with `which ruby`, which will output your Ruby path and version number.

## Install bundler
Gem is the Ruby package manager that we’re going to use to install bundler…a package manager. This is necessary to use Jekyll and useful for any other Ruby project.

```
gem install bundler
```

## Install Composer
A necessity for modern PHP development.

```
curl -sS https://getcomposer.org/installer | php
```

Add it to the executable path.

```
sudo mv composer.phar /usr/local/bin/composer
```

Test it on the command line.

```
composer --version
```
