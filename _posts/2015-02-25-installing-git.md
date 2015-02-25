---
layout: post
title: "Installing Git"
description: Installing git on windows and linux systems
headline: 
modified: 2015-02-26
category: Version Control Systems
tags: [git,github,vcs]
imagefeature: some.jpg
mathjax: 
chart: 
comments: true
featured: true
share: true
---

When I started my web development, I used to share my code zipping it and sending it over the mail to receiver or used FTP to transfer files seamlessly. But this used to be tiresome, slowed down my learning curve. I couldnt rollback when something went wrong. So, versioning of the product or software was needed, and I found git. This article covers the installation of git and getting familiar to git.

Install git bash right away from [here](http://git-scm.com/downloads) for your operating system.

Lets consider that you have an [account](http://github.com) on github, or a account on gitlab hosted by some organisation.

For *Windows* follow the onscreen instructions in the installer, choose *Run git from the Windows Command Prompt* for accessing git commands from windows command prompt along with git bash.

For *Linux* use your package manager to install git. 

On debian/ubuntu :

> apt-get install git

On Fedora :

> yum install git

Done. You now have a vcs command line application. To confirm your installation, you can use `git --version` which prints the version of the application.

Configuring git for the first time, you need to enter these commands only for the first time, after installing git in your system.

Add _username_:

> git config --global user.name "username"

Provide your github/gitlab username.

Add _email_:

> git config --global user.email mail@kranthikiran.in

Provide your email id.

To check your list of configurations, use

> git config --list

Now, to use git behind proxy, you should set http.proxy and https.proxy variables as follows:

> git config --global http.proxy http://proxy.server.com:3128
> git config --global https.proxy https://proxy.server.com:3128

proxy.server.com can be for example 172.30.0.16

This article now leaves you with git CLI installed on your system and you can teach git yourself using this [tutorial](http://try.github.io/) created by github. After this tutorial, follow these steps:
<ol>
<li>create a test repository on github</li>
<li>git init it in your system</li> 
<li>set a remote url</li>
<li>Edit or add some file(use git add <filename>)</li>
<li>check status(use git status command)</li>
<li>commit the file(s)( use git commit -m "commitmessagehere")</li>
<li>push the commit.(git push)</li>
</ol>
 These are the steps followed when you first create a repository. Once you have pushed your first commit then you can use steps 4 through 7 for tracking changes to your code and controlling the versions of your software. 

 Further articles shall contain insights on fixing conflicts, fixing common problems, proxy issues etc.