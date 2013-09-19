Mac Setup for Rails Developers
==============================

This a guide to help you get setup for Rails development on a Mac. I had to do this recently for someone else, so I figured I would document the process.


XCode and Developer Tools
-------------------------

Install the latest [XCode](https://developer.apple.com/xcode/). *Make sure to also install command line tools*.


HomeBrew
--------

[HomeBrew](http://brew.sh/) is a package manager for OS X, which we'll use to install our command-line applications.

Follow instructions at bottom of Homebrew page to install it

To install HomeBrew, run the following at the command line:
```
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```

Then close terminal and re-open (restart terminal).


Now run ```brew doctor``` to make sure everything is okay. If there's no error, skip this next step.

  * echo export PATH='/usr/local/bin:$PATH' >> ~/.bash_profile
This will create a .bash_profile file which gets read every single time you open a new terminal window. From here on in, you can either restart terminal to apply the latest changes in this file, or run 'source ~/.bash_profile'
* brew install wget

brew update

notes:
* homebrew is a package manager for osx. it's generally used to install command-line applications conveniently.
* brew packages are downloaded and installed in /usr/local/Cellar/ by default, and symlinked into /usr/local/bin. This folder will not be overriden the next time you update OSX
* command-line executables are searched in order of PATH directories; try running echo $PATH to see the ordering of folders (expand on this with subl and git as an example)

some stuff on how formulas work and how easy they are to make.

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