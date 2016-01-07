---
layout: post
title: "Automated Git Deployment"
description:
headline:
modified: 2016-01-06
category: Version Controlling
tags: [web,git,gitlab,github,gitautodeploy,version control system]
imagefeature: https://cloud.githubusercontent.com/assets/1056476/9344294/d3bc32a4-4607-11e5-9a44-5cd9b22e61d9.png
mathjax:
chart:
comments: true
featured: true
share: true
---

Hi! I use Github/Gitlab and Bitbucket with Git CLI for most of the projects to do version controlling. To understand what is version control, I suggest you go through this [link](http://producingoss.com/en/vc.html)

While working on one of the projects, one of my client wanted to edit few meta tags and titles of few pages in the website right away from the Github/Gitlab and wanted to see the changes on the live server. So, I thought of writing a script to automate this idea. But before I started writing the script, I made a google search and found that there is already a OpenSource package available which implements quite exactly what I wanted. I found [`Git-Auto-Deploy`](http://github.com/olipo186/Git-Auto-Deploy.git) which is a python based server that can be used to setup Automated Git deployments.

I have cloned the repository right away and started experimenting with it. Its very simple to setup and follow the instructions as provided in the README file.

Follow the instructions and test it with a webhook. While using this script behind a proxy, one might face issues with a blocked ssh url. When we push to the repository for the first time, if the proxy blocks in pulling on the server, we can see a message like "Unable to find the repository *ssh-url* in the config". We need to copy that `*ssh-url*` and update it in the `url` field of `GitAutoDeploy`. Now, we need to use the insteadOf feature provided by `git`. Use the following command to convert `git@` to `http` urls.

>git config --global url.http://github.com/.insteadOf git://github.com/

Replace `github.com` with your remote host.

I hope, there is a better way to handle this issue, but this is something I figured out and made it work like a charm.

I have used `GitAutoDeploy` in most of my University's internal servers to perform Automated Git Deployments using our private Gitlab. This really made my life peaceful and clients life easy.

Thanks for reading the post, do comment if you think there is a better way to do Automated Git Deployment.
