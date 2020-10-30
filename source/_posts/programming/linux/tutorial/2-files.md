---
title: GNU/Linux Introduction Chapter 2
categories: 
- Programming
- Linux
tags:
- Programming
- Linux
language: en-US
---

<div align="center" style="font-size: 33px"><b>
    Chapter 2: Files
</b></div>

## File Formats

Well I have to say that there is actually no such things called "format" for Linux. For Linux, it's all about if it can be executed or not. Life is easier for Windows, as most executables in Linux have no file extension.

You **are** able to execute any file in Linux, and the OS will decide if it is executable or not. In Linux, the most common executable file format is the Executable and Linkable Format, **ELF**. Let's take the hexdump of `gcc` for example.

```
  Offset: 00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F 	
00000000: 7F 45 4C 46 02 01 01 00 00 00 00 00 00 00 00 00    .ELF............
00000010: 02 00 3E 00 01 00 00 00 60 6F 40 00 00 00 00 00    ..>.....`o@.....
```

The first 16 bytes are the magic header of ELF executables, and you can see the `ELF` ASCII characters from bytes 1 to 3. The OS will use the Magic to identify if it is an executable or not. Also, text files are executable. They can be used to execute shell commands, and we will talk about that later.

Anyways, to execute a file, you have to change the permission of the file first, and we have to know what file permissions are, and what the hell does `ls -la` really tell us.

## File Permission

Remember the output from `ls -la`? If not, just run the same command again. Your output will be similar to something like

```
total 12
drwxr-xr-x  3 root    root    4096 Aug  4 21:23 .
drwxr-xr-x 20 root    root    4096 Aug  5 20:08 ..
drwxr-xr-x 21 rebuild rebuild 4096 Sep 25 20:15 rebuild
```

Forget about the first line `total 12` for now. It is related to some OS knowledge on the file system. Now, we shall really focus on understanding the other lines describing the details for those files and directories. It is really easy to understand the last 4 columns representing month, day, time of modification, and the name of that file. The 5<sup>th</sup> column represents the size of the file, in bytes. Here, each directory is a file that takes up 4 KiB of the disk (or memory) space.

> Note: I add "memory" because directories such as `.` and `..` may not really exist on disk. They might be put in memory and used by OS directly from memory. The size of a directory will always be 4 KiB because the file representing a directory contains metadata about the files in that directory (inodes and file names). The smallest size for a block in the disk is 4 KiB, so directories will take up 4 KiB initially. However, if there are too much contents in that directory, the size of the directory file will grow large. I created a directory with 10,000 files inside using `touch {1..10000}`, and that directory is of size 155648 bytes, or 152 KiB. That is exactly 38 blocks.

Now let's check the first column, that is, the **permissions** of the file. It is represented here in `ls` by the 10 characters, e.g. `drwxr-xr-x`. When we want to understand this, we have to seperate it into 1-3-3-3, that is, `d rwx r-x r-x`.

The first character, `d`, indicates that this file is a directory. Other valid options are

- `-`, meaning a regular file
- `l`, meaning a **symbolic link**
- `c`, meaning **character device**
- Others we don't care about for now<sup>[1](#Notes-and-References)</sup>.

Well that's easy. Now come tricky stuffs. The **real** permissions for files and directories. 

### File Permissions

The permissions of a file are represented in `ls` by the latter 3 groups consisting of 3 characters, such as `rwx`. They are indicative of **read**, **write**, and **execute** permissions, respectively. If the character is `-`, it means that the specific permission is denied. And for the meaning of the 3 groups, see the table below.

<table style="table-layout: fixed;">
    <thead>
        <tr>
            <th colspan=3><div align="center">File's owner<div></th>
            <th colspan=3><div align="center">Other people in file's group<div></th>
            <th colspan=3><div align="center">Anyone else<div></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center">r</td>
            <td align="center">w</td>
            <td align="center">x</td>
            <td align="center">r</td>
            <td align="center">w</td>
            <td align="center">x</td>
            <td align="center">r</td>
            <td align="center">w</td>
            <td align="center">x</td>
        </tr>
    </tbody>
</table>

Usually, a file's owner is in the file's group. The two information can be seen from the 3<sup>rd</sup> and 4<sup>th</sup> column of the output of `ls -l`. 

| Character | Meaning       |
| --------- | ------------- |
| `r`       | Read file     |
| `w`       | Write to file |
| `x`       | Execute file  |
| `-`       | No permission |

Note that the `root` user in Linux has the highest privilege, so `root` can execute any command and do whatever it want on any files regardless of the file permission.

### Directory Permissions

Similar to file permissions, the latter 3 groups for directory permissions also consists of `rwx`, and the first character in `ls -l` will always be `d`. However, here the meaning is slightly different.

| Character | Meaning                                                     |
| --------- | ----------------------------------------------------------- |
| `r`       | Read directory content using e.g. `ls`                      |
| `w`       | Make changes on directory, e.g., creating, moving, deleting |
| `x`       | Go into directory using `cd`                                |
| `-`       | No permission                                               |

There are, though, other permission types. For the "anyone else" group, there is the sticky bit, `T` and `t`. Also there are the `setuid` and `setgid` bit, `S` and `s`. I will not talk about them here.<sup>[2](#Notes-and-References)</sup>

### Octet Representation

Here we can see that regular file permissions can be represented by 9 flags in 3 groups. Therefore, for each group, we can let the flags be bit flags and form a octet. For example, `rwx` will be `0b111` in binary and thus `7` for this octet; `r--` will be `4`, and `---` will be `0`. Therefore, combining 3 groups together, we will have 3 octets, and we will use this to change the file permission later. The `d` character representing if the file is a directory is ignored here because it is more of a "property", not "permission", of a file.

Some examples:

```
drwxrwxr-x  ->  775
-rwxr-xr-x  ->  755 (most common)
-r--r--r--  ->  444
-rwx--x---  ->  710
```

## Changing File Permission

Ignoring the special permissions that we will not cover, only you and `root` (admins) can change the permission of files owned by you. We need the `chmod` command, standing for **ch**ange **mod**e, to change the permission of a file.

First let's use the octet representation to change the permission. We use the command `chmod <permission> <file>`. For example, to give full permission to a file, we use `chmod 777 <file>`. 

```
$ ls -la a.py                               # ~/test
-rw-r--r-- 1 me   me   63 Sep 22 13:18 a.py
$ chmod 777 a.py                            # ~/test
$ ls -la a.py                               # ~/test
-rwxrwxrwx 1 me   me   63 Sep 22 13:18 a.py
```
Always, you can set the file permission as you want using this way. 

Another way to set permission using `chmod` is when you want to easily add or delete a permission. We will use this format of the command: `chmod [ugoa...][+-=][perms...] <file>`, which is called a symbolic format. First, let's look at the `[ugoa]` part. It controls which groups of permission are to be changed.

- `u` stands for the first group, which is the current user.
- `g` stands for the second group, which is other users in the file's group.
- `o` stands for the third group, which is anyone else.
- `a` stands for all three groups.

Then, the `[+-=]` part.

- `+` is for adding permissions.
- `=` is for setting permissions.
- `-` is for removing permissions.

The final part `[perms...]` is the permission part. You can use the abbreviation `rwx`, and one or more can be applied. For example,

- `a+x` means adding execute permission to everyone
- `o-r` means removing read permission of people outside the file's group.
- `ugo+rwx` is the same as `a+rwx`, or `777`, which is giving all permissions.

## Notes and References

1. If you want to know more, you can execute `info coreutils ls "what information"` and refer to the documentation.
2. See [1].

<hr>
<h6 align="right"><a href="/programming/linux/tutorial/3-io">Next</a> | <a href="/programming/linux/tutorial/preface">Home</a></h6>