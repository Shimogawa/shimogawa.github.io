---
title: GNU/Linux Introduction Chapter 1
categories: 
- Programming
- Linux
tags:
- Programming
- Linux
language: en-US
---

<div align="center" style="font-size: 33px"><b>
    Chapter 1: Introduction
</b></div>

## The Ubuntu Operating System

During this course, I will introduce you to the Ubuntu system which is (I think) the widliest used Linux based OS for non-commercial use. However, if you are using Mac OS, it's fine to just use this OS provided by Apple since the toolset (maybe not provided by GNU I think) are mostly POSIX compliant.

Installing Linux on Windows could be a troublesome thing, but now Windows provides [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10). If you don't want WSL, just use a virtual machine (though they both work the same way; the only difference is that a virtual machine provides graphics). If you install a version with graphics (with desktops, etc.), just open the Terminal after you successfully log on the OS.

For your reference, the latest Ubuntu image could be found on its [website](https://ubuntu.com/download), and for virtual machine holder, I suggest [Oracle VirtualBox](https://www.virtualbox.org/) or [VMWare](https://www.vmware.com/).

If you are in China, please download the `.iso` image from [Netease](http://mirrors.163.com/ubuntu-releases/).

## The File System

**The file system in Linux is beautiful.** Someone once asked me how devices are connected to the OS. When thinking about Windows, we don't really know how to answer this question. Devices are managed by a whole bunch of drivers and softwares in the OS on Windows. However, in Linux, you can have a direct feeling that these devices **are indeed** installed on your PC. Though they are still managed by the Kernel, but **you** as a user is able to see it. 

Take the console for example. The console is an I/O device (actually most devices perform I/O). On Windows you don't surely know where `stdin` and `stdout` come from. On Linux, the console is a file at the location `/dev/tty` (or the standard streams `/dev/{stdin,stdout,stderr}`). You can perform input and output on this file _just like how you read or write a file_. Therefore, learning the file system first in Linux is necessary and important.

Interestingly enough, you can even check your mouse movement in the console with the help of device files (of course in a system supporting mice). Just open your terminal and input the following command.
```bash
sudo cat /dev/input/mice
```
Then move your mouse and see what is printed on your terminal. The `cat` (not dog) command stands for "con**cat**enation", and you can use it to print out content of a file. The `sudo` command stands for "**s**uper **u**ser **do**", and it is used to get the root privilege to run the command. This device file `/dev/input/mice` is endless since the computer don't know when you will end moving your mouse, so `cat` will keep printing (seemingly) random bytes when you move your mouse. More on this later when we talk about I/O.

> Note: <span style="color: #6788ea">We will not talk about mounting and other advanced stuff here, only the basic things that will later make you comfortable using Linux or Unix like systems.</span>

The file system in Linux works like a tree (called a file system tree). Unlike Windows where you have several disks with their own separate file system (called a file system forest), Linux file system has only exactly one **root** node of the tree (it is a directory), which is `/`. Everything is the children of `/`. For example, if you have a file called `a.txt` under `/`, you will write its path as `/a.txt`. On Windows, similarly, if you have a file `a.txt` under `C:\`, you will write its path as `C:\a.txt`. 

If we keep appending paths like this, we call that an **absolute path**. Consider the following structure:
```
                /
         _______|_______
        /       |       \
      home    a.txt     bin
       |               __|__
       me             /     \ 
       |            gcc     cat
    .bashrc
```
We can see here that if we want to get the file `gcc`, we need to use its absolute path `/bin/gcc`. For `.bashrc`, it's `/home/me/.bashrc`. Similarly, for directories, it's the same (actually directories themselves are files containing information about the directories!). For example, the absolute path for `me` is `/home/me`.

However to keep a file system structure is not that easy. What if you are in a directory and you want to go to its parent? Is it necessary to use absolute path every time when you only want to access a file in your current path? Here comes the solution. In **every** directory (which is a subtree of in the file system tree), there exist two special directories, `.` and `..`. Check this by doing

```bash
ls -la /home
```

This commandline will list all items in the directory `/home`. The `ls` command stands for "**l**i**s**t contents". The flags `-la` mean to list all items with details. This is a useful command. A notice here is that files and directories in Linux are **hidden if the name starts with `.`**. Therefore actually, `.` and `..` are hidden directories. Only with the flag `-a` to `ls` can we see them. If we use `ls -l` only, we will not be able to see the hidden files. Following is the output for me.

```
total 12
drwxr-xr-x  3 root    root    4096 Aug  4 21:23 .
drwxr-xr-x 20 root    root    4096 Aug  5 20:08 ..
drwxr-xr-x 21 rebuild rebuild 4096 Sep 25 20:15 rebuild
```

We will talk more about this output later, but our focus now is to see that there are `.` and `..`. `.` points to this directory itself, and `..` points to the parent directory. It's a good question that since `/` has no parent, how can it have the `..` link? Well, the developers of Linux have decided that `..` in `/` also points to itself, and that solves the problem.

## Terminal and Shell

It's really confusing to understand what is a "terminal" and what are "shells". I found this answer clear and interesting.

> **Shell** is a program which processes commands and returns output, like `bash` in Linux.
> **Terminal** is a program that runs a shell, in the past it was a physical device (Before terminals were monitors with keyboards, they were teletypes) and then its concept was transferred into software , like Gnome-Terminal.<sup>[1](#Reference)</sup>

Actually there are plenty of shells in Linux, such as the GNU `bash`, `sh`, and others like `zsh`, `csh`... They basically run executables for you and generates output and return codes. And since you want to see these outputs, you need a terminal to run shells. Actually `tty` which means a console (basically a terminal) comes from the word **t**ele**ty**pe which is a very very old hardware (screen) that displays the output from the shell. 

## Reference

1. [What is the difference between Terminal, Console, Shell, and Command Line?](https://askubuntu.com/a/507138)


<hr>
<h6 align="right"><a href="/programming/linux/tutorial/2-files">Next</a> | <a href="/programming/linux/tutorial/preface">Home</a></h6>
