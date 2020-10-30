---
title: GNU/Linux Introduction Appendix A
categories: 
- Programming
- Linux
tags:
- Programming
- Linux
language: en-US
---

<div align="center" style="font-size: 33px"><b>
    Appendix A: Shell Commands
</b></div>

Here I provide some useful commands and executables in shell which is portable on Linux or Unix based systems (Ubuntu, Debian, MacOS, Cygwin, ...). For detailed description on how to use these commands, use `<command> --help`, `man <command>`, `info coreutils <command>`, or google them.

Some of the executables (such as `gcc`) does not come with some systems themselves. You might need to install them first. Just google `<OS> how to install <package>`.

| Executable / Command | Stand For                                                 | Short Description                                                    |
| -------------------- | --------------------------------------------------------- | -------------------------------------------------------------------- |
| `bash`               | **B**ourne-**A**gain **sh**ell                            | The most used shell                                                  |
| `bg`                 | **b**ack**g**round                                        | Make a process run in background                                     |
| `cat`                | con**cat**enate                                           | Show contents of a file or stdin                                     |
| `cd`                 | **c**hange **d**irectory                                  | Change directory                                                     |
| `chmod`              | **ch**ange **mod**e                                       | Change access permissions of files                                   |
| `chown`              | **ch**ange **own**er                                      | Change the owner of files                                            |
| `cp`                 | **c**o**p**y                                              | Copy a file to another path                                          |
| `diff`               | **diff**erence                                            | Check the difference between files                                   |
| `echo`               | **echo**                                                  | Print something                                                      |
| `fg`                 | **f**ore**g**round                                        | Bring a background job to foreground                                 |
| `gcc`                | **G**NU **c**ompiler **c**ollection                       | The compiler collection for C, C++, and Fortran                      |
| `grep`               | `g/re/p`: **g**lobal **r**egular **e**xpression **p**rint | Search in files or streams for lines that match a regular expression |
| `id`                 | **id**entity                                              | Print user and group information                                     |
| `jobs`               | **jobs**                                                  | Check status of jobs running in current terminal                     |
| `kill`               | **kill**                                                  | Send a signal to a process (not necessarily `SIGKILL`!)              |
| `ls`                 | **l**i**s**t contents                                     | List contents in a directory                                         |
| `man`                | **man**ual                                                | Manual for commands                                                  |
| `mv`                 | **m**o**v**e                                              | Move a file or directory to another path                             |
| `ps`                 | **p**roce**s**s                                           | Check processes running in the system                                |
| `pwd`                | **p**rint **w**orking **d**irectory                       | Print the full path of current directory to stdout                   |
| `rm`                 | **r**e**m**ove                                            | Delete a file                                                        |
| `scp`                | **s**ecure **c**o**p**y                                   | Copy or transfer files to a remote endpoint                          |
| `sed`                | **s**tream **ed**itor                                     | Edit a file or stream with command-line                              |
| `sh`                 | **sh**ell                                                 | The most basic shell with few features                               |
| `sleep`              | **sleep**                                                 | Suspends program execution for a specified time                      |
| `ssh`                | **s**ecure **sh**ell                                      | A remote login interface and shell                                   |
| `su`                 | **s**witch **u**ser                                       | Switch to and login as another user                                  |
| `sudo`               | **s**uper **u**ser **do**                                 | Execute a command in elevated privilege (root)                       |
| `tar`                | **t**ape **ar**chive                                      | Pack files and have the ability to compress                          |
| `top`                | **t**able **o**f **p**rocesses                            | A real-time process monitor                                          |
| `touch`              | **touch**                                                 | Create a file, or change and modify timestamps of a file             |
| `tr`                 | **tr**anslate                                             | Substitute contents, or select or delete contents from input         |
| `vi`                 | **v**isual **i**nstrument                                 | A visual editor                                                      |
| `vim`                | **`vi`** i**m**proved                                     | A better visual editor                                               |
| `which`              | **which**                                                 | Identify the location of a given executable in `PATH`                |

<hr>
<h6 align="right"><a href="/programming/linux/tutorial/preface">Home</a></h6>