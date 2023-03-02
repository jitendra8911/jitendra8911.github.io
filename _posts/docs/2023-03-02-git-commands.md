---
layout: post
date: 2023-03-02 07:21
title: "ReactJS cheatsheet"
category: docs
tags:
- documentation
  comments: true

---

useful git commands

<!--more-->

## setting up ssh authentication

[Guide to set up ssh authentication](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

## pushing to github without ssh key

For every push we don't want to authenticate using username and password. This is annoying. This is where ssh comes handy.
Once ssh authentication is setup, run the following command:

git remote set-url origin git@github.com:<Username>/<Project>.git

Next time, when you push, git will not ask for username and password