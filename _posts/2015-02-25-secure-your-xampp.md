---
layout: post
title: "Secure your xampp"
description: 
headline: 
modified: 2015-02-25
category: Web Development
tags: [xampp,php,security,phpmyadmin]
imagefeature: img.jpg
mathjax: 
chart: 
comments: true
featured: true
share: true
---
The previous article on installing xampp covered how to install xampp in Windows or debian based operating system. This article is a continuation of the previous article and shall be used to cover security aspects of xampp stack.

Start the xampp using xampp control panel in Windows(use the commands for linux), and start apache web server and phpmyadmin. Check that your servers are started and no ports are occupied by any other application before starting these servers from xampp. If you need to change the ports, go to config option under server, and carefully change the port numbers to some unused port numbers.

>You can use *netstat -a -n* command to check port numbers being used by various applications.

So, inorder to secure xampp, you can set password so that no one else can access unless they know your secure password. Otherwise, anyone in the same network as you are, can access your xampp directory, phpmyadmin, ftp etc. by knowing your IP address, and if it is insecure, then you can get locked out from using it, for example: changing user permissions in phpmyadmin etc.

Here a list of missing security in XAMPP:
*The MySQL administrator (root) has no password.
*The MySQL daemon is accessible via network.
*ProFTPD uses the password "lampp" for user "daemon".
*PhpMyAdmin is accessible via network.
*The XAMPP demopage is accessible via network.
*The default users of Mercury and FileZilla are known.

To setup a password:

In *Linux*:
{%highlight sh%}
sudo /opt/lampp/xampp security
{%endhighlight%}
and follow the onscreen instructions.

In *Windows*:

>Use  *http://localhost/security/* to open security console, and fix it by entering passwords for xampp, mysql and phpmyadmin.

So, this should leave you with all green icons with secure when you goto security tab in http://localhost/xampp. No one on your network except you can now use your xampp stack. 

Further articles shall cover deploying web applications.