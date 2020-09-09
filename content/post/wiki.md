---
title: "Wiki"
date: 2020-09-09T14:53:12+08:00
lastmod: 2020-09-09T14:53:12+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: ""

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
autoCollapseToc: false
postMetaInFooter: false
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""

---

# First Try

原理应该是每次删除public，并将其从工作树上清除，删掉`.git`中痕迹；
然后重新添加工作树到public目录，重新确认删除public下可能有的文件；
执行`hugo`重新编译，进入public切换至gh-pages分支，添加所有文件并提交；
最后在执行完脚本后，进行推送

```bash
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

# 设置成功后，只需要执行以下命令，修改message就可以
# 进入public目录分支自动切换
hugo
cd public && git add --all && git commit -m "Publishing to gh-pages" && cd ..
```


<!--more-->
