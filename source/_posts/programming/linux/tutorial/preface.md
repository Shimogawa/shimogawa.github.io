---
title: GNU/Linux Introduction
categories: 
- Programming
- Linux
tags:
- Programming
- Linux
language: en-US
---

<div align="center" style="font-size: 33px">
    GNU/Linux Introduction
</div>
<div align="center" style="font-size: 20px">from the perspective of I/O
<br>
<img src="https://img.shields.io/badge/Rebuild-714026292-orange" />
</div>

## Preface

I decided to write an introduction to the GNU/Linux based operating systems (I will call them "Linux" for the sake of simplicity) because throughout my undergraduate study and current working, I kind of begin to understand really how operating system really works and how the GNU tools (well basically they are just command-line commands, or if you like, executables and built-ins) designed for the Linux Kernel make life easier. I am definitely **not** an expert in any of operating systems or kernels, nor am I an experienced programmer, but I find out that Linux commands starts to become a part of life (even when I use Windows, I will use Linux commands provided by [cygwin][cygwin]), and that everyone in the region of computer science should learn (at least a bit) about Linux.

<p>
    <details>
    <summary></summary>
    <p>Well another reason for me to write this is that my girlfriend has just become a freshman in Computer Science...❤️</p>
    <p>Knowledge keeps driving humanity. Any that might help, I will give. Just like the Ash in Dark Souls who will never give up knowing the faintness of Fire.</p>
    </details>
</p>

I think here I should tell you a little bit about Linux. If you only talk about plain Linux, it is a **kernel**, rather an OS. The GNU project made tools around the Kernel. And...

> So it happened that at the same time there was a project for a kernel without tools (Linux), and a project with all the tools but without a kernel (GNU). As both were written with the same UNIX mindset it was possible to combine them into a full operating system which people aptly called "GNU/Linux". <sup>[1](#References)</sup>

I won't talk so much about what exactly is Linux or who made Linux (sorry Linux Torvalds) because my aim is not here. You really should check out the [Wikipedia page][linux_kernel_wiki] if you are really interested. Instead, I would like to introduce you the GNU/Linux, on Ubuntu, with its command-line interface and command-line tools _from the perspective of I/O_. (However I/O is much too important for me to tell you about the whole thing in this short intro.)

Though an introduction, this tutorial still targets people with a few experience in Computer Science. If you are a beginner or a new-comer, please be sure that your basic knowledge in either programming or operating systems is solid enough. I will not teach anything basic about how to program in Linux.

Enjoy!

## Index

- [**1 Intro**](/programming/linux/tutorial/1-intro)
- [**2 Files**](/programming/linux/tutorial/2-files)
- [**3 IO**](/programming/linux/tutorial/3-io)
- [Appendix A: Shell Commands](/programming/linux/tutorial/commands)

## Contributions

If you have anything to supplement or you find any error, just comment below the web page, or contact me via `admin@rebuild.moe`!

## References

1. [Why do people call Linux a kernel rather than an OS?](https://unix.stackexchange.com/questions/94402/why-do-people-call-linux-a-kernel-rather-than-an-os)


[cygwin]: https://www.cygwin.com/
[linux_kernel_wiki]: https://en.wikipedia.org/wiki/Linux_kernel
[repo]: https://github.com/Shimogawa/shimogawa.github.io
