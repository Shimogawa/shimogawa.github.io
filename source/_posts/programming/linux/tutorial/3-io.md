---
title: GNU/Linux Introduction Chapter 3
categories: 
- Programming
- Linux
tags:
- Programming
- Linux
language: en-US
---

<div align="center" style="font-size: 33px"><b>
    Chapter 3: I/O
</b></div>

## Standard I/O

Maybe you have heard of standard in or out (`stdin` or `stdout`) before. If you use Java, you must be familiar with two streams: `System.in` and `System.out`. They are I/O streams onto the terminal, or `tty`. I don't want to confuse you as well as myself, so for now let's just say the standard I/O prints and gets text to and from the console screen.

### File Descriptors

When it comes to I/O, you might first think of files. In Linux, files are accessed by **file descriptors**. The file descriptors are integers given by the kernel when you want to access (say, read or write) a file. The descriptor allows you to have access to the file as well as its information or metadata. For example, in C, if you want to open and read from a file **with system calls** (instead of using standard libraries that makes the call and wrap around for you), you will use the function `int open(const char *pathname, int flags)` and `ssize_t read(int fd, void *buf, size_t count)`. For more you can read `man 2 open` and `man 2 read`. An example program will be

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>      // file control flags

int main() {
    int fd = open("/home/rebuild/a.txt", O_RDONLY);
    char buf[1024];
    ssize_t bytes_read;
    while ((bytes_read = read(fd, buf, 1024)) > 0) {
        // ...
    }
    return 0;
}
```

Now, I will introduce 3 special file descriptors: 0, 1, and 2. They are reserved and will always exist. They represent `stdin`, `stdout`, and `stderr`, respectively. File descriptor 0 is read only, and file descriptors 1 and 2 are write only. You can easily use them since you don't need to manually open them. Just use them as simple as

```c
#define STDOUT 1

// ...

write(STDOUT, "hello, world!", 14);
```

In Linux, standard I/O have another appearance as device files so that standard I/O can also be interpreted as file I/O. Go to `/dev/fd` using `cd`. If you list files using `ls -la`, there must be 3 entries as follows.

```
lrwx------ 1 root root 64 Oct 29 14:18 0 -> /dev/pts/0
lrwx------ 1 root root 64 Oct 29 14:18 1 -> /dev/pts/0
lrwx------ 1 root root 64 Oct 29 14:18 2 -> /dev/pts/0
```

They actually all point to `dev/pts/0`, which stands for the **p**seudo **t**erminal**s** (pty for short). This is the number 0 of the ptys. There may be many ptys under this folder, and you can use `tty` command to check which pty are you using for your own shell. It's just a readable and writable device file representing the terminal. We will talk more on this when we use redirection in the next chapter.

With this knowledge in mind, let's learn some I/O in shell.

## I/O in Shells

> For anything related to shell starting from this point, I will use Bash as an example. Check your shell using `echo $SHELL`. If it's not `/bin/bash`, please type `/bin/bash` to switch to Bash.

### Redirecting Output

Now we know that I/O includes all of files and standard streams (and also devices). Now, let's manipulate I/O in shells and forget about programs for now.

I have never told you how to write to a file before. Let's suppose for now that we don't have text editors, not even `vim`, `emacs`, `nano`, or `ed`. How to write to a file? Well, we have to use **output redirection**. The operator for this operation in shells is `>`. For example, if we want to write `Hello, world` to a file `a.txt`, we can simply use `echo -n "Hello, world" > a.txt`. The `-n` option means that no additional new line character `\n` will be printed. Here, `echo` will print whatever you wrote to `stdout`, and `>` will **redirect** `stdout` to whatever follows, `a.txt` in this example. 

Let's do one more useful example. Say a program will print huge amounts of useless information to the screen and you don't want to see them. `head -n 10 /dev/urandom` will be great example. The `head` command by default reads the first 10 lines from a file (to peek the head of a file). You can specify the number of lines to read by using the `-n <number>` option. `/dev/urandom` is a special file (called a character special **device**) that will give out random bytes when read from. 10 lines from random byte stream will be a lot. Just pretend that this is a program you want to execute. How to make the output disappear? Here, we need another special device file called `/dev/null`. From its name we can know clearly that it represents a black hole. Everything written to this file will go away. Therefore, we have the solution: `head -n 10 /dev/urandom > /dev/null`. 

Now let's see some advanced usage of redirection. We learned the 3 special file descriptors previously. Let's use them here. First, we can specify which stream to redirect to. `1>` will redirect `stdout(1)`, and `2>` will redirect `stderr(2)`. The previous `>` is just shorthand for `1>`. Let's choose a program that will print to both `stdout` and `stderr`. Most error messages will go to `stderr`. Let's use `ls`. If you `ls` a file that doesn't exist, it will report error. First, choose a file that exists in your current directory and a name that doesn't exist in your directory. For me, I have `a.txt` in my directory, but no `b.txt`. Then, if I execute `ls a.txt b.txt`, it will print

```
ls: cannot access 'b.txt': No such file or directory
a.txt
```

The first line is from `stderr`, and the second line is from `stdout`. Let's try to hide `stderr` using knowledge we have. Yes, `ls a.txt b.txt 2>/dev/null` is correct. It will then only output `a.txt`. Similarly, `ls a.txt b.txt 1>/dev/null` will only output `ls: cannot access 'b.txt': No such file or directory` to `stderr`. Now here comes the question. If a program only accepts `stdout`, how do I redirect `stderr` to `stdout`? The first option is using the knowledge we have. Remember `/dev/fd/1`? It's a file! We can use `2>/dev/fd/1`! Run `bash -c "ls LICENSE a.txt 2>/dev/fd/1" > /dev/null` to check that no output is generated. If you only run `bash -c "ls LICENSE a.txt" > /dev/null`, you will also get the error message. However using this name is too long for file descriptors. Therefore, if you want to access a file descriptor for redirection, you can use the shorthand `&<fd>`. In previous example, we can just write `bash -c "ls LICENSE a.txt 2>&1" > /dev/null`, and `2>&1` is always the best way to redirect `stderr` to `stdout`. 

### Pipes

First of all, most GNU utility programs which accept files as inputs accept standard input. Let's take `cat` as an example. The command `cat` is for printing contents of a file. It can print also the standard input. If you just type `cat` into the terminal and then you type something and hit <kbd>↵ Enter</kbd> (Windows) or <kbd>↵ Return</kbd> (Mac), you will see the exact same thing you typed in the output! But how is this even useful? Well, maybe not for `cat`, but for many other programs. 

Let's check again the `head` program. Suppose you have a file `numbers.txt`, which consists of the numbers 1 to 10, each on a line. If you execute `head -n 5 numbers.txt`, you will get 1 to 5 as expected. Also, if you run `head -n 5` alone, and you input 5 lines, they will be printed out. Now, let's say you have a command that will output a lot of information. Let's use `ip` for an example. `ip a` will show you all the network configurations for your computer. However, sometimes the output is very long. What if I only want the first result? Yes! Let's use `head`! But wait... How to read the output from another program into the input of `head`? The answer is **pipe**! The format of pipes is `<command1> | <command2> | ... | <commandN>`. 

Continue with the last example. We will use `ip a | head` to show the information of the first 10 lines. Next, I will introduce you a super useful command: `grep`. I plan to introduce this command gradually throughout this course, but here I will tell you the basic usage of it. Basically, it will show lines that contains a given regular expression. You can grep a file using `grep <regex> <file>...`, and here we want to use it to find lines within output of another command. Let's check the model name of our CPU cores! The information about CPUs are stored in the file `/proc/cpuinfo`. If we only use grep, we can use `grep "model name" /proc/cpuinfo`. Then, let's get the content of the file using `cat` and pretend that it's not reading from a file, which is something `grep` can do. We can use `cat /proc/cpuinfo | grep "model name"`. More useful scenario is when we want to check the processes running in background. We have to use `ps` command standing for **p**roce**s**s. We can see **all** processes running by `ps -ef`. Let's check if there is any `python` running. The command is `ps -ef | grep python`. If nothing show up, then no python is run on your computer. You can then check for other processes. 

The last thing I want to tell you in this chapter is an interesting one-liner<sup>[1](#Notes-and-References)</sup> to generate random strings in Bash. It's useful when you want to generate temporary IDs or passwords. 

```bash
cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 13 ; echo ''
```

You can remove the `echo` part to remove the new line character. For `tr`, it is used to select out the characters in the given regex pattern. `-c` for `head` is for number of characters. By this line, you can generate a 13-character long random string. An example usage of this command is as follows.

```bash
tmpfile=$(cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 13)
hostname -i > $tmpfile
ping -c 1 $(cat $tmpfile)
rm -f $tmpfile
```

The grammar `$(...)` is just getting the output of a command as a string. A newer syntax for this is backticks `` `...` ``. This is an unnecessarily complicated example just to show you how to use this. Maybe a better one is just `ping -c 1 $(hostname -i)`.


## Notes and References

1. [Unix: How to generate a random string?](https://unix.stackexchange.com/a/230676)


<hr>
<h6 align="right"><a href="#">Next</a> | <a href="/programming/linux/tutorial/preface">Home</a></h6>
