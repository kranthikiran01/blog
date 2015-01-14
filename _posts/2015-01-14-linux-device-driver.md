---
layout: post
title: "Building Linux Device Driver - Part 1"
description: "This post shall throw some insight into building a virtual device driver in linux"
headline: 
modified: 2014-07-23
category: Operating Systems
tags: [linux,device driver,virtual device,character device driver]
imagefeature: some.jpg
mathjax: 
chart: 
comments: true
featured: true
share: true
---

Hello reader!! I know its too bad to start the second post with geeky stuff but I felt this topic should definitely be blogged since its cool, building a device driver, whoa...I got excited when I was taught about this topic in my class.

Ever thought how a computer monitors various drivers attached to it? Obviously there must be some software which does that. 

Yes, device driver is a software which drives, monitors, controls, directs and monitors the devices that are under computer's command. Consider, the device driver here as a car driver. What does a car driver do? He drives it, controls, manages and directs it. So, driver must be programmed/taught to do that. The device is now analogous to a car. You must not have thought that device driver is actually a software, right?

Often, we also see drivers which are automated. That is, a device can either be controlled directly by the **software** i.e Device driver or the device can be controlled by a **device controller**(another piece of hardware ) which in turn is controlled by a software. We observe the latter case in bus drivers.
Example for Device controllers: HDD controllers, Display controllers, Audio controllers, USB controller etc.

Now, when we want to install the device driver in the system, if you are a windows user you must have seen a prompt while installation saying 

> The driver has been installed, system reboot is required to activate the driver. Please restart.

This is annoying, if you dont want the system to reboot ever. For example, a live server should never be restarted unless it is critical, and this is not critical. Also, there can be device with embedded operating system which strictly prohibits soft shutdown or soft reboot once it is live. What will you do in this case? This is where __LINUX__ comes in handy.

__Linux__ has the feature of loading and unloading the drivers dynamically. So, it wont require any stupid reboots. Commands like `insmod`, `lsmod`, `modprobe` and `rmmod` are used to load and unload the drivers on the fly. If you look in the `lib/modules/linux-headers-<version>/kernel` directory, you can find various modules which contain kernel objects. These kernel objects are actually the device drivers provided by linux build. The **insmod** command is used to load or insert a kernel object. **lsmod** is used to list the loaded modules. **rmmod** is used to remove a loaded module. **modprobe** is an advanced command with more features which is a partial mix of **insmod** and **rmmod** command features.

So, the drivers in linux modules contain two parts - The init or constructor part and The exit or destructor part. These parts donot have relevance in dynamically loading or unloading but play a cool role during kernel compilation and system bootup. These parts are functions marked with `__init` and `__exit` macros which are copied to `init` and `exit` blocks of kernel image. During kernel compilation, all the driver's functions marked with __init and __exit are loaded into init and exit blocks of kernel image. All functions with __init are executed once during system bootup and the kernel will free up RAM by freeing the init block. Similarly, all functions in `exit` are executed during system shutdown.

You might have wondered how do we write a driver program. We write these programs in Standard C language with linux headers. Oh, what are linux headers? When we write regular programs in C language, we use the headers which are present in `/usr/include` where as writing device driver programs require different headers which are present in the linux build or source. So, we need a different compiling procedure when we compile our driver program saying our driver needs headers from the linux build and not the usual headers. We use `Makefile ` for this purpose. More on this in a meanwhile.

Now, lets try writing our first driver template program using the headers in linux build. The headers are taken from `/usr/src/linux-headers-<version>`. The `<version>` can be known by using `uname -r` command.

Source for mydriver.c
{%highlight c %}
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/init.h>

static int __init mydriver_init(void){
	printk(KERN_INFO "Driver registered\n");
	return 0;
}

static void __exit mydriver_exit(void){
	printk(KERN_INFO "Driver says goodbye!\n");
}

module_init(mydriver_init);
module_exit(mydriver_exit);

MODULE_LICENSE("GPL");
MODULE_AUTHOR("KRANTHI");
MODULE_DESCRIPTION("Testing the driver template for creating,loading and unloading modules");
{%endhighlight%}

mydriver_init function is the part which gets executed when driver is loaded. Think of this as constructor. The linux kernel programming has some objective touch to the C as we observe from this example.
Similarly, mydriver_exit function is executed when driver is unloaded.
We convey this to the kernel by using module_init and module_exit methods which take the function names as argument.

The `MODULE_LICENSE()` with "GPL" is used since, few linux distros like ubuntu or mint might ask for authorized or signed drivers. These are called vendor provided drivers. If we try to load our driver, we will get error while make or in the syslog saying tainted kernel, which means kernel is in a state that is not supported by community which develops it. So, we use GPL which stands for General Public License, stating that this driver is being built for OpenSource use and can be used port of Linux.

`MODULE_AUTHOR` and `MODULE_DESCRIPTION` are fields for describing the drivers author and its description.

Now, that we wrote the template driver.c program, we should compile. As said earlier, we should use Makefile to do that.The following can be used for Makefile. Note that the file should be named as `Makefile` with no extension or prefixes or suffixes. Otherwise, your make command wont work.
This is for linux versions > 3. Also, I found problems with 64bit linux distro in combination with GCC version 4.9.2 . Try upgrading to `4.8.2` from `4.9.2` for fixing the unmet dependencies in 64bit linux machines.
{% highlight c %}
obj-m := driver.o
KERNEL_DIR := usr/src/linux-headers-$(shell uname -r)/
all:
	make -C $(KERNEL_DIR) SUBDIRS=$(PWD) modules
clean:
	make -C $(KERNEL_DIR) SUBDIRS=$(PWD) clean
{% endhighlight %}
`all` and `clean` are called targets. Note that Makefile is case sensitive. Tab and spaces are totally different for it. I had to headbang several times when my make didnt work for quite a while.
`$(shell <command>)` is used to get command result in Makefile. `obj-m` is used for the list of what kernel modules are to be built. Here, driver.o is the object used to build the modules. We can have multiple objects using `obj-m += driver1.o` and `obj-m += driver2.o` for two drivers driver1.c and driver2.c programs.

After this, type `make` in the directory containing driver.c and Makefile. You should see something like this.
![Figure 1]({{ site.url }}/images/linux-drivers/fig1-linux-driver-part1.png)

`dmesg` is the command used to view the output of our printk(stands for `print from kernel`). These printk outputs are stored in `/var/log/syslog` file. Any command with `|` operator and head -5 or tail -5 suffix will yield the top 5 or bottom 5 rows of the result. Note that `rmmod` command should be supplied an argument with no .ko extensions where as `insmod` requires the argument to contain the .ko extension.

Thats all for this post, explore the syslog file and play with the loading, reading and unloading of kernel objects. The next post shall throw insight on creating a virtual character device and writing drivers for it. Feel free to comment any issues you face while trying this tutorial.

Stay tuned for the part 2 of building linux device drivers!