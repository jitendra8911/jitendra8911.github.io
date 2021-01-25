---
layout: post
date: 2021-01-23 6:35
title: "Troubleshooting Jekyll Errors"
category: docs
tags:
- documentation
comments: true

---
Are you facing issues while installing gem dependencies? Are you running into issues while serving jekyll?
Do you want to have different version of ruby installed for different projects? Then good news! You are in the right place. 
In this article I will explain how to fix all such issues.

<!--more-->

If are just looking for how to spin up a new jekyll blog, install ruby/gem/bundle in your project directory you can skip the following section and head 
to [Useful Jekyll commands](#useful-jekyll-commands)

It's almost been two years since I wrote my last post. Whoooah!! Last week I was going to write an article on one of the hardest
coding problem I ever solved in my life [Advent Of Code 2020](https://adventofcode.com/2020/day/20){:target="_blank"}. I am going to talk about my experience in solving this problem in another article.
But the point is, when I started running the website on my local, I ran into some local environment issues. I was scratching my head and trying to get my head around the errors
I was getting but with little luck. Finally after thoroughly deep diving into what jekyll/gem/bundle/rbenv is and how they work, 
I was finally able to figure out how to overcome such type of issues. In this article I am going to talk about what issues I faced and how I have overcome such type of issues.


## Jekyll errors

You might be encountering various errors including but not limited to following:

* `could not find i18n-0.9.5 in any of the sources`
* `Bundler could not find compatible versions for gem "ruby"`
* `Could not find concurrent-ruby-1.0.5 in any of the sources`
* `bundler failed to load command jekyll`
* `require: cannot load such file -- rexml/parsers/baseparser`
* `cannot load such file webrick`

After encountering the above errors and doing some research I found that installing rbenv and using it to install all other tools such as
ruby/gems/bundler required for a project is going to fix the above errors. The following section explains briefly about importance of rbenv and bundler


## Importance of rbenv

The main use of the tool rbenv is to maintain different versions of ruby for different projects. Some projects might
require ruby 2.7 whereas other projects might need ruby 3.0. In order to install different versions of ruby in your machine and switch between them, rbenv as far
as I know is the only tool available to do so. The errors mentioned in [Jekyll errors](#jekyll-errors) could have been a result of having
incompatible versions of jekyll/ruby/bundler or any other gems installed in your machine globally. If instead you use rbenv to switch to a specific ruby version
pertinent to your project, you can get rid of those errors. For more information on rbenv please visit
[rbenv github page](https://github.com/rbenv/rbenv){:target="blank"}

## Importance of bundle

Whereas rbenv is used to determine which ruby version to use and which bundle is installed implicitly within the ruby, bundle is used to
install specific gems for the jekyll project such as jekyll itself or other gems such as html-proofer or webrick etc. For more information
on bundle visit [bundle tutorial](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/){:target="blank"}

## Useful Jekyll Commands

If you are starting a jekyll project from scratch, start from step 1. If you already have a project but are running into the above mentioned [Jekyll errors](#jekyll-errors)
then start from step 10.

1. Install rbenv: `brew install rbenv`
2. Run this command and follow instructions: `rbenv init`
3. Install specific ruby version by doing: `rbenv install 3.0.0`
4. Go to the directory where you want to create jekyll project and issue: `mkdir project-name`
5. initialize bundler: `bundle init` 
6. Setup ruby version you want your project to use by issuing: `rbenv local 3.0.0`
7. configure bundler installation path: `bundle config set --local path 'vendor/path'`
8. Add jekyll as dependency to our project by running: `bundle add jekyll`
9. If you want to create default them and pages to your website run: `bundle exec jekyll new --force --skip-bundle`
10. If you already have any gems installed under the vendor/path, delete them as we want to install the gems freshly.
11. Install gems under local path vendor/path by running: `bundle install`. If you are running into any issues here, make sure
you are using the correct ruby version for the project by issuing: `rbenv local 3.0.0` and go to step 10.
12. Serve the site by running: `bundle exec jekyll serve --livereload`. If you run into any errors such as missing gem such as webrack, 
add it to Gemfile and try running again. The issue should be resolved.


