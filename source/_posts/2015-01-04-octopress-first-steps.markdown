---
layout: post
title: "Octopress: first steps"
date: 2015-01-04 19:30:28 +0100
comments: true
categories: 
- Octopress
- configuration
- install
- git
- GitHub
- Ruby
- Gems

---
# Octopress #

[Octopress](http://octopress.org) 3.0 is a framework to generate static blog web site. It is developed with Ruby and other tools like Rake.
Octopress is derived from GitHub [Jekyll](https://github.com/mojombo/jekyll) framework used with [GitHub Pages](https://pages.github.com) service and is compatible with most of its plugin. Octopress would be a better and more friendly Jekyll 

Blog site lifecicle is base on writing markdown document, generate a static site and the publish its deployment artifact to some kind of web server.

Octopress is delivered with its own set of plugin to aid blogger to write better article. The framework focuses on the drafting of technical articles based on code publication.

Octopress have a MIT licence

[This](https://github.com/imathis/octopress/wiki/Octopress-Sites/_edit) is the list of sites based on Octopress.

## Install ##

There are two prerequisite: **Git** and **Ruby 1.9.3**.

Clone Octopress project from imathis github repository:

	git clone git://github.com/imathis/octopress.git octopress 

from inside the new created directory
	
	gem install bundler

to do this on Mac OSX you need administrator privileges for writing in Ruby install directory (sudo).

What is bundler?
>Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed.
[bundler.io](http://bundler.io)

In `octopress` cloned directory there is a `Gemfile`, so you have to install declared gems for octorpress with this command

	bundler install

you are asked to type your password to install gems...
Dependencies are now installed, so install the **default theme** (classic) that for many reasons is the best:

	rake install

Rake is a ruby application that substitute the `make` executable in ruby environment. It is a software task management tools and is able to build ruby applications with `Rakefile` and `.rake` configuration files. 

To know what task are available in you project directory type:

	rake --tasks

this reveals that 
	
*rake install[theme]            # Initial setup for Octopress: copies the default theme into the path of Jekyll's generator*

All installed themes are in `.themes/classic/` directory.

Octopress is installed.

#### Install Sequence

	git clone git://github.com/imathis/octopress.git octopress
	cd octopress/
	sudo gem install bundler
	bundle install
	rake install
	rake setup_github_pages
	rake generate
	rake deploy
	rake preview (optional)
	git add .
	git commit -m 'primo post'
	git push origin source


If you are restoring an existing project from GitHub

	git clone --branch source git@github.com:baselibera/baselibera.github.io.git OctopresClone 
	rake setup_github_pages (for new directory correct git configuration)

Create and modify post and pages

	cd _deploy
	git commit -a 'publish new content' 

Resolve conflicts

	git merge
	git push origin master

Source are not updated too.

cd to root octopress install directory
	git add .
	git commit -m 'new page <aboutme>'

When update an installation modifed elsewhere you can found some natural conflict in some file.

	git pull origin master
	
To resolve:
edit file manually to resolve conflict, and then

	git add atom.xml
	git add sitemap.xml
	git commit -m 'manual merge'
	git pull origin master



## Editing Lifecicle ##


	rake new_page[] or rake new_post[]
	rake generate
	rake deploy
	rake preview  and rake watch (optional)

`master` branch is automatically pushed every time rake deploy is executed.
`source`branche needs a manual prepare and push of artifacts, even in the same manner if with non conflicts:

from root install directory:

	git add .
	git commit -m 'message'
	git push origin source
	

### GitHub  Pages ###
One of the deploy option Octopress present is based on [GitHub Pages](https://pages.github.com).
This GitHub service permit to publishing a personal website or a project presentation website. In the first case you will have to create a repository for a project with the same name as the username more `.github.io` postfix.
In my case this became **`baselibera.github.io`**. When create this kind of repository make it public and do not check the Initialize this repository with a README`.

After created verify access from a web browser at `http://baselibera.github.io`.
Its SSH URL is: git@github.com:baselibera/baselibera.github.io.git

To configure your Octopress installation to deploy on GitHub Pages execute this command:
	
	rake setup_github_pages

From rake tasks help we have that: 

*rake **setup_github_pages**[repo]  		# Set up _deploy folder and deploy branch for Github Pages deployment*

Launching the GitHub Pages setup it ask you about the URL, in my case git@github.com:baselibera/baselibera.github.io.git.

the task act for:

- set repository url at git@github.com:baselibera/baselibera.github.io.git
- add a remote git@github.com:baselibera/baselibera.github.io.git as origin
- set `origin` as default remote
- rename Master branch to 'source' for committing your blog source files
- remove old `deploy` directory and create a new one
- in the deploy directory initialize an empty Git repository in /Users/jolab/octopress/_deploy/.git/
- commit the master 
- add the index.html to git control

all these comments are outputs on console, the execution at least says:
*Now you can deploy to git@github.com:baselibera/baselibera.github.io.git with `rake deploy` *

But there is nothing to really deploy to GitHub Pages in _deploy directory.
First you must generate something:

	rake generate
	
This genearte files of your static blog to `/public` directory. Now deploy it:

	rake deploy
	
After commit all:
	
	git add .
	git commit -m 'first octopress commit'
	git push origin source

Now you have two **branch** of your GitHub Pages repository

- **master**: for publish contents
- **source**: source from wich your public and then your _deploy directory are populated after generation and deploy. 

#### How to clone an existing GitHub Pages Octopress source

	git clone --branch source git@github.com:baselibera/baselibera.github.io.git OctopressGitHub
 

### Heroku ###

### Rsync ###

This is a tool to syncing your local Octopress deploy directory with your hostinf server. This tool require SSH access to your server.
 
## Blogging ##

There are two main default type of content in Octopress:

- posts
- pages

### Posts

So there are two rale tasks to help to create theese:

	rake new_post["My post title"]

this task create the **`source/_posts/2015-01-04-octopress-how-to-begin.markdown`** file.
 
`source/_posts/' directory is the repository for contents and file names contains generation date and have a markdown extension. This is one of the main reason I have explored Octopress: *Markdown native contents management*.

This file contain a **yaml** front matter that is used by jekyll to process file.

	---
	layout: post
	title: "Octopress: how to begin"
	date: 2015-01-04 10:55:55 +0100
	comments: true
	categories:
	---

The most are clear. Categories can be expressed with a single string, with an array of strings: [catname1, catname2, catname3], or as a markdown list

	- catname1
	- catname2
	- catname3


### Pages ###

The main difference with post is that pages are not listed in home page as blog articles.
With:
 
	rake new_page[whoami]

we can generate an Octopress page in

	source/whoami/index.markdown

Also this is a markdown file and have a fron matter in **yaml**.

It is accessible with `http://baselibera.github.io/whoami/` 

If you use instead:

	rake new_page[about/page.html]
	
will generated the `source/about/page.html` file.
It will be accessible as `http://baselibera.github.io/about/page.html`


