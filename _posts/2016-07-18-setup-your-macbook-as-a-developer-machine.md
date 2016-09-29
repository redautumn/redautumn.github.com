---
title: "Setup your Macbook as a developer machine"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-07-18 10:48:26 EDT
---

Create this article to summarize my scirpts to setup my Macbook:

## Install ruby and rvm

```
curl -sSL https://get.rvm.io | bash -s stable --ruby
# install bundler
gem install bundler
# Add the following line into .bash_profile or .zshrc
source ~/.rvm/scripts/rvm
```

## Setup VIM

```
brew rm vim vim python
brew install python
brew install vim --with-override-system-vi
```

#### Note: if python3 is not installed or configured as default

```
brew install macvim --with-cscope --with-lua --with-override-system-vim --with-luajit --with-python
brew linkapps macvim
```

## Intellij-IDEA

```
brew cask install intellij-idea-ce
```

## Reference

- [My Mac OS X development setup](http://www.codejuggle.dj/my-mac-os-x-development-setup/)
- [Install Ruby on Rails 5.0 · Mac OS X El Capitan](http://railsapps.github.io/installrubyonrails-mac.html)