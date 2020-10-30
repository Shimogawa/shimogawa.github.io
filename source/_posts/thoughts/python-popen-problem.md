---
title: A Python Popen Problem
date: 2020-10-27 22:08:44
categories:
  - Programming
tags:
  - Programming
  - Problems
  - Thoughts
language: en-US
---

This is a problem found during my work in some company. I would like to share it and give some solutions or debug processes.

## The Problem

The original problem is that a complex testing framework hangs for no reason. In my first step for debugging, I immedialy checked the process tree using `pstree -ap <pid>`. It shows that the process hang on its `ssh` subprocess. The command is something like `ssh <username>@<ip> command` and is just a normal ssh execution command. It should never go on forever, since this command usually needs only 5 seconds.

It's hard, but I finally check the code and found the Python script for making this subprocess. The code is as follows.

```python
import subprocess

# ... code ...

try:
    proc = subprocess.Popen(["ssh", "<username>@<ip>", "<command>"],
                            stdout=subprocess.PIPE,
                            stderr=subprocess.STDOUT)
    proc.wait()
    output = proc.stdout.read()
    retcode = proc.returncode
    return retcode, output
except:
    # ... code ...
```

I tested the code on my machine, and it worked fine! How is it possible! Why will it hang there? Especially since the process is not over, it hangs at the `wait` call. Why is that?

## Debugging

Well it's easy to guess that the problem in in the output stream. My first guess is that it needs to wait for all output in the `PIPE` buffer to be cleared, but since the code works on other places, this seems to be implausible. I decided to check explicitly for the buffer.

Fortunately, we have `/dev/urandom` to test for outputs. For controlling the output size, I used both `head` and `dd` (for controlling output more precisely). Let's write a code and test it. Note that Python 3 is used for this test. Both Linux and Windows with bash can be used for this test.

```python
import subprocess

block_size = 65536

proc = subprocess.Popen(["bash", "-c", f"dd if=/dev/urandom bs={} count=1 2>/dev/null"],
                        stdout=subprocess.PIPE,
                        stderr=subprocess.STDOUT)
proc.wait()
output = proc.stdout.read()
retcode = proc.returncode
print(len(output))
```

If we run this test, we can see `65536` printed as expected. However, let's change `block_size` to 65537, or any value above that. Now we have a program that will never stop running! Now we can say that the buffer for `subprocess.PIPE` is exactly 65536. Therefore, we now know why the problem appears. The process is waiting for the buffer to clear up and only after it can stop running. Also, as long as the total amount of received bytes exceeds 65536, the program will hang, even if block size is so small and count is large, i.e., `dd if=/dev/urandom bs=1 count=65537 2>/dev/null` will hang as well.

## Solution

The solution is so easy that I am surprised. Just swapping two lines and the problem is solved:

```python
import subprocess

block_size = 65536

proc = subprocess.Popen(["bash", "-c", f"dd if=/dev/urandom bs={block_size} count=1 2>/dev/null"],
                        stdout=subprocess.PIPE,
                        stderr=subprocess.STDOUT)
output = proc.stdout.read()
proc.wait()   # put it here!
retcode = proc.returncode
print(len(output))
```

Now, the program will first read all the bytes until the end, and then wait for the program to exit instead of waiting for someone to take away the output from the buffer! It's a hard problem with an easy solution. I hope it will never happen again.

Testing is hard, but it's even harder to test a testing framework!
