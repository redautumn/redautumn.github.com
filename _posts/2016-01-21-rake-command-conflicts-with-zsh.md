---
title: "rake command conflicts with zsh"
layout: single
tags: speeches
subclass: 'post tag-speeches'
categories: 'blog'
navigation: True

comments: true
date: 2016-01-21 15:45:28 EST
---

I am using zsh as my default shell. However, when I tried to use rake command to create new post (The Rakefile is cloned from [jekyll rake files] (https://github.com/avillafiorita/jekyll-rakefile)). e.g. 

```
rake create_post[, 'my new post']
```

However, when I run this command in zsh, it always throws some errors. 

```
zsh: bad pattern: create_post[,
```

After a bit of Google search, I found I am not alone. And here is a blog [How To Use Arguments In a Rake Task](https://robots.thoughtbot.com/how-to-use-arguments-in-a-rake-task) for rescue. Basically what need to do is:
Add the following option in your .zshrc file:

```bash
unsetopt nomatch
```

And then, you can do this in termal:

```bash
rake create_post\[, 'my new post']
```

Also try to record some of the jekyll commands here for later reference:

```bash
# start the preview server
bundle exec jekyll server
```




