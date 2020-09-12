---
title: "How to deploy github pages with hugo"
date: 2020-09-09T14:53:12+08:00
lastmod: 2020-09-09T14:53:12+08:00
draft: false
keywords: []
description: "how to deploy github pages with hugo"
tags: ["hugo", "tutorial"]
categories: ["tutorial"]
author: "ztf88"
---

## Install hugo

> Hugo would be installed easily to windows and linux

- [Repo](https://github.com/gohugoio/hugo)

- [Releases](https://github.com/gohugoio/hugo/releases)

### Windows

- Extra "hugo_extended_0.74.3_Windows-64bit.zip" 
- Put "hugo.exe" to MSYS64 "msys64/usr/bin" which path had been added to $PATH 
 
```bash
$ hugo version
Hugo Static Site Generator v0.74.3/extended windows/amd64 BuildDate: unknown
```
### Linux

```bash
mkdir $HOME/src
cd $HOME/src
git clone https://github.com/gohugoio/hugo.git
cd hugo
# go install
# installing with extended could solve some mistakes about scss 
# "extended" info could show in "hugo version" 
# hugo will be installed to $GOPATH
CGO_ENABLED=1 go install --tags extended
```

## Some commands from hugo docs and more 

- [how to host on github with hugo](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

```bash
# hugo version
# hugo new site your_awsome_site
# git clone https://github.com/olOwOlo/hugo-theme-even themes/even
# cp themes/even/exampleSite/config.toml .
# cp themes/even/archetypes/default.md ./archetypes
# hugo server
# mv themes/even/.git themes/even/dotgit
# git config user.name "john"
# git config user.email "john@example.com"
# echo "public" >> .gitignore
# git status
# git add . && git commit -m "initial hugo blog"
# # create a new repo named "yourname.github.io"
# # if you don't create a readme.md, you will see some tips about "how to add
# remote repo to you local repo"
# git remote add origin https://github.com/yourname/yourname.github.io.git
# git pull 
# git status

git checkout --orphan gh-pages
git reset --hard
git commit --allow-empty -m "Initializing gh-pages branch"
git push upstream gh-pages
git checkout master
rm -rf public
git worktree add -B gh-pages public upstream/gh-pages
hugo
cd public && git add --all && git commit -m "Publishing to gh-pages" && cd ..
git push upstream gh-pages
# generate and push
hugo
cd public && git add --all && git commit -m "Publishing to gh-pages" && cd ..
# "--all" will push both master and gh-pages to github
git push --all 

```


## Scripts 

> put "publish_to_ghpages.sh" to your repo, your blog will be published easily.

1. `clean_master.sh`

```bash
#!/bin/bash

git add ./content/post/* && git commit -m "update"
```

2. `publish_to_ghpages.sh`


```bash
#!/bin/sh

if [ "`git status -s`" ]
then
    echo "The working directory is dirty. Please commit any pending changes."
    exit 1;
fi

echo "Deleting old publication"
rm -rf public
mkdir public
git worktree prune
rm -rf .git/worktrees/public/

echo "Checking out gh-pages branch into public"
git worktree add -B gh-pages public upstream/gh-pages

echo "Removing existing files"
rm -rf public/*

echo "Generating site"
hugo

echo "Updating gh-pages branch"
cd public && git add --all && git commit -m "Publishing to gh-pages (publish.sh)"

#echo "Pushing to github"
#git push --all
```

## Some hugo commands

```bash
hugo server
hugo
hugo new /content/post/new-title.md
```
