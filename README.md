# Doing it Right

This is an opinionated guide to getting a Rails dev environment setup quickly on a Mac. This is written assuming you have Lion (10.7+) or later as your operating system.
If you have the choice, always choose a Mac for your dev environment. It's just easier. Linux is okay too.

I'm writing this guide from the point of view of someone setting up a clean system. If you already have some of this software installed, you'll have to adjust accordingly. If you use RVM or MacPorts, you'll need to fully uninstall those before continuing as they're incompatible with rbenv and HomeBrew, which are my preferred tools.

This guide assumes that you're using bash shell, which is the default shell for the OSX Terminal application. I also assume that you use .bash_profile to setup PATH and other environment variables. If you use a different bash config file, be sure to substitute it where appropriate below.

## XCode and Developer Tools

Install the latest [XCode](https://developer.apple.com/xcode/). **Make sure to also install command line tools, which is an option during the install process**.


## HomeBrew

[HomeBrew](http://brew.sh/) is a package manager for OS X, which we'll use to install our command-line applications. It's a much more convenient alternative to compiling the code ourselves from source (or using MacPorts).

To install HomeBrew, copy, paste and run the following at the command line:
```
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```

Then close terminal and re-open it (restart terminal).

Now run ```brew doctor``` to make sure HomeBrew installed correctly. You should see something like this:

![Running brew doctor](assets/homebrew.png)

This is a problem. Let's fix this by moving the bin directory that HomeBrew sets up for us ahead of every other folder specified in PATH. Run the following:

```
echo export PATH='/usr/local/bin:$PATH' >> ~/.bash_profile
```
This will create a .bash_profile config file which is read and executed each time a new terminal is opened. To apply changes made to this file, you can either restart terminal (ghetto mode), or run ```source ~/.bash_profile```.

Test this out by installing wget via HomeBrew: ```brew install wget```.
Now run ```brew update``` to get the latest HomeBrew formulas.


### An Aside: Why PATH Order is Important

Command-line executables are searched by going through each folder in the PATH variable, one by one in the order listed. As soon as an app with the same name is found, it stops searching the rest of the folders. OSX comes with built-in apps (and you might have your own apps installed prior to this), but we often want to use newer versions instead. To see the PATH directories, run ```echo $PATH```.

HomeBrew packages are downloaded and installed in /usr/local/Cellar/ by default, and symlinked into /usr/local/bin. This folder will not be overriden the next time you update OSX to its next feline avatar. Nice!


For the reader:
How do I get a list of homebrew packages that are installable?
How do I get a list of currently installed homebrew packages?
How do I update an existing package?

Git

git comes with mac os x but it's typically and old version. Let's get a newer version.
brew install git

git --version
  * should be > 1.8

Sublime Text Editor (command line)
http://www.sublimetext.com/docs/2/osx_command_line.html

Installing sublime command line
Skip this if you have another preferred command line text editor.

We're going to install this in the homebrew bin director instead of ~/bin as stated on the sublime text website.
ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl


rbenv
https://github.com/sstephenson/rbenv

brew install rbenv
This installs rbenv, a lightweight tool to help you manage different version of ruby. OSX comes with an old version of ruby, and we'll generally want to have our own versions of Rails (particularly 3.2.13 and 4.0.0).

brew install ruby-build

subl ~/.bash_profile

add ' eval "$(rbenv init -)" ' to the end of ~/.bash_profile and save.

Then either restart Terminal or run 'source ~/.bash_profile' to apply the changes.

If you look at your path (echo $PATH) you should see that reloading your bash_profile has inserted .rbenv/shims to the beginning of your $PATH variable.

To install ruby 2.0.0-p247 (substitute this for the latest stable version of ruby indicated on ruby-lang.org):
rbenv install 2.0.0-p247

You can install other rubies this way as well. This may take some time.

After this finishes, you can setup your global (default) ruby by typing:
rbenv global 2.0.0-p247

Note that you can override this per project (folder). See https://github.com/sstephenson/rbenv#choosing-the-ruby-version for more information.


RubyGems
rubygems ships with ruby 2.0.0. If you need to install this manually, see http://rubygems.org/pages/download

Run:
gem update --system to get the latest version.


MySQL (server)

brew install mysql

After installation you get a message showing you how to run mysql automatically when your system boots. If you don't want it to startup on boot, you can run the following commands to start and stop mysql server:

mysql.server start
mysql.server stop

mysql -uroot to connect to the server using the command line, but we'll be using sequel pro which is a really nice GUI to interact with the database in general.


Sequel Pro (MySQL client)
http://www.sequelpro.com

Download and drag this to Applications in order to install.
This is the best MySQL client for Mac.

Go to the Socket tab and enter the following to connect:

Name: localhost
Username: root

and then Connect. You're now connected to your MySQL database and can add, view, delete databases like a boss.



Installing Rails locally

You need to have Rails locally in order to create new Rails projects. After the project is created (or if you're working with an existing rails project), you'll always be using the bundled versions of Rails specific to your project.

gem install rails -v 3.2.13 (this is the latest stable version of Rails 3)
gem install rails (get the latest version of Rails, which at the time of writing is Rails 4)

For Mac, never run sudo in front of these commands.

You can look at your gems using gem list. Verify that Rails is there and the version is correct.

Now run source ~/.bash_profile so that rails is visible.

Let's install Rails 4 as well. This is just
gem install rails

source ~/.bash_profile again.


Making a new Rails project
By default any Rails commands now will use the latest version of Rails. Some assignments assume Rails 3 though.

To make a new Rails 4 project, cd into your projects folder:

rails new app_name
or
rails _3.2.13_ app_name


the run rails server. visit http://localhost:3000 in your browser. congrats.


GitHub Installation
* hook git up to your existing GitHub account
* setup ssh keys so you don't have to type your password in every single time

(see brian's thing)


Resources
http://blog.teamtreehouse.com/installing-ruby-rails-and-mysql-on-os-x-lion


git (newer version)
  * config stuff

homebrew
rbenv
ruby
rails 3, 4 (local install)
imagemagick
mysql



ssh key generation


software (optional)

* sublime - setting up subl for command line use
  * package manager
* postgres.app
* sequel pro