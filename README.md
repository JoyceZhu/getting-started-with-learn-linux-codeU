# Getting Started with Learn on Linux

## Overview

At this point, you probably already have an environment setup that you like – we don't want to mess with that. We do, however, want to make sure that your environment can talk to Learn.

## TL;DR

What follows will walk you through installing a few necessary libraries on your system. If you trust us, you can just run the following (or the appropriate substitutes for your OS) in your terminal:

![Do you trust me?](http://i.giphy.com/voF2A48B0XQje.gif)

```bash
sudo apt-get update
sudo apt-get install git
sudo apt-get install -y libssl-dev libreadline-dev zlib1g-dev

git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bash_profile

# (restart your shell)

rbenv install 2.3.0 # this will take a while
rbenv global 2.3.0

gem install learn-co
learn hello

# If you run into an issue about a missing .netrc,
# run the following:

touch ~/.netrc
chmod 0600 ~/.netrc

# and then try `learn hello` again

sudo apt-get install default-jre
sudo apt-get install default-jdk
sudo apt-get install ant
```

Read on if you're the detail-oriented type.

## <3 Your Package Manager

You probably already know and love your package manager – we just wanted to remind you.

For what follows, we'll assume that you're running on a system that has `apt`; modify the commands as necessary if you're more the `yum` type (for example).

First, let's make sure we're up to date:

```bash
sudo apt-get update
```

## Install git

Now we're going to install `git`. We'll cover `git` in more detail soon, but for now know that it's version control software – it has fancy ways of keeping track of your work that allow you to selectively apply changes or to revert to a prior state. Pretty sweet.

`apt` makes installation easy:

```bash
sudo apt-get install git
```

And you're done!

## Install Ruby

### Prerequesites

Ruby requires a few additional libraries to install. Run

```bash
sudo apt-get install -y libssl-dev libreadline-dev zlib1g-dev
```

to get them.

### The Main Attraction

To install Ruby, we're going to use a version manager called [`rbenv`](https://github.com/rbenv/rbenv). The reason that we're adding this bit of indirection is that your system probably already has its own version of Ruby – we don't want to mess with it.

(Note: Some of you might be complaining about installing Ruby for a series of Java lessons. Learn's software depends on Ruby, and while we won't be covering it much here, Ruby is an interesting language and one that's used all over the place in software engineering (especially web development). You don't have to like it, but you'd do well to learn it.)

Feel free to follow along with the official instructions: https://github.com/rbenv/rbenv

First let's clone the `rbenv` source using `git`:

```bash
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
```

Then add `~/.rbenv/bin`to your `$PATH` so that you can execute `rbenv` at the command line. (If you're not using bash as your shell, use the config file that's appropriate (e.g., `~/.zshrc` if you're using zsh).)

```bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
```

The [`rbenv` documentation](https://github.com/rbenv/rbenv#understanding-path) has a brief and excellent section on `$PATH` if you're unsure how that works.

Run `~/.rbenv/bin/rbenv init` for specific instructions to add `rbenv` to the available commands. Go ahead and follow those instructions; we'll wait right here.

![](http://i.giphy.com/3oEdv9pgtUVVYdpaY8.gif)

Install the [`ruby-build`](https://github.com/rbenv/ruby-build) plugin. This way we can install Ruby versions with `rbenv install x.y.z` and be on our way.

```bash
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
```

Finally, install Ruby 2.3.0

```bash
rbenv install 2.3.0
rbenv global 2.3.0
```

You can check your installation with `ruby -v` – it should print something like `ruby 2.3.0p0 (2015-12-25 revision 53290)`.

## Install Learn

Ruby packages are called gems; a local Learn CLI application is one of them. Let's install it with

```bash
gem install learn-co
```

Then run `learn hello` to get the ball rolling.

Note: If you get an error about a missing `~/.netrc` (or `/home/[your username]/.netrc`), you can just create the file and give it the correct permissions:

```bash
touch ~/.netrc
chmod 0600 ~/.netrc
```

Then run `learn hello` again and follow the instructions.

## Install Java and Ant

Compared to install Ruby, installing [Java](https://java.com/en/download/) and [Ant](http://ant.apache.org/) (a Java build tool) is easy. Just run

```bash
sudo apt-get install default-jre default-jdk ant
```

Bada-bing!

## Resources

- [DigitalOcean's guide to installing git on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-14-04)
- [DigitalOcean's guide to installing Ruby (on Rails) on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-with-rbenv-on-ubuntu-14-04); **ignore the Rails bits**
- [gorails.com's guide to installing Ruby (on Rails) on Ubuntu 14.04](https://gorails.com/setup/ubuntu/14.04); **ignore the Rails bits**
