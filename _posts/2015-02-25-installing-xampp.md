---
layout: post
title: "Installing XAMPP stack"
description: Installing xampp on windows and linux systems
headline: 
modified: 2015-02-25
category: Web Development
tags: [php,phpmyadmin,xampp,htdocs]
imagefeature: some.jpg
mathjax: 
chart: 
comments: true
featured: true
share: true
---

Hello reader, this article serves as a little guide for setting up XAMPP stack on your system for developping web applications using PHP and MySQL.

Inorder to install XAMPP, first find out the architecture of your system, it should be one of 32bit(x86) or 64bit system. On Windows, you can find it from system info usually available in properties from right click of My Computer. If you are in debian based linux system, then you can find it in system details.

Based on the above details, choose the package and download it from [apachefriends](https://www.apachefriends.org/download.html)

For *Windows* systems:
Downloads the executable(.exe) file. Life is so easy in windows systems, hence you just need to do the next next next process, but choose the installation directory to be accessible by you with ease(installation at C:/xampp is recommended).

For *Linux* systems:
Downloads the file with extension (.run). Thanks to developers of xampp that linux has got a GUI based installer. Before you can run it, you should first ensure that its file permissions have been set properly and you have enough permissions to run it.
So, modify its permissions using chmod system command. Open your terminal, cd to the downloaded package and type:
{%highlight sh%}
sudo chmod 777 ./xampp-linux-<version>-installer.run
{%endhighlight%}
Now run the installer using:
{%highlight sh%}
sudo ./xampp-linux-<version>-installer.run
{%endhighlight%}
You can look at _/opt/_ folder for lampp(aka xampp - l for linux <3 ).

For *both* systems:
Done. You now have xampp installed. You can run the xampp control panel and start it.
Goto your browser and type in localhost/xampp to confirm your installation of xampp.
Note for _linux_ systems:
Incase you have _mysql_ installed prior to installation of xampp, you have to stop it before you run xampp. To stop mysql, run the following command,
{%highlight sh%}
sudo service mysql stop
{%endhighlight%}
Now, start the xampp using following commands from terminal,
{%highlight sh%}
sudo /opt/lampp/lampp start
{%endhighlight%}
Replace start with restart to Restart the xampp stack, replace start with stop to Stop the Xampp stack execution.

ApacheFriends has good FAQ, you can get that at [FAQ](https://www.apachefriends.org/download.html)
Stay tuned for coming posts to activate the security features in xampp(Not necessary if you are on a development machine, but very essential in production servers).