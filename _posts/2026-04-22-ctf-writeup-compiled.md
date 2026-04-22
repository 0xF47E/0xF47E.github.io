---
layout: post
title: "CTF-Writeup: THM - Compiled"
date: 2026-04-22 17:30:00 +0100
url: https://tryhackme.com/room/compiled
difficulty: easy
author: me
tags: CTF
---

The challenge was to analyze compiled binary. 

After downloading it and executing the binary, it prompted for a password. 

Therefore I decided to analyze the binary with [Ghidra](https://github.com/nationalsecurityagency/ghidra) to decompile it and look at the code.

![Ghidra](/images/compiled/Ghidra.png)

It shows that password needs to equal `_init`.

The input is supplied with scanf. There was a pattern used I did not know (`DoYouEven%sCTF`). Therefore I looked for the scanf documentation in the manpage.

```
The format string consists of a sequence of directives which describe how to process the sequence of input characters. If processing of a directive fails, no further input is read, and scanf() returns. A "failure" can be either of the following: input failure, meaning that input characters were unavailable, or matching failure, meaning that the input was inappropriate (see below).

A directive is one of the following:

• A sequence of white-space characters (space, tab, newline, etc.; see isspace(3)). This directive matches any amount of white space, including none, in the input.
• An ordinary character (i.e., one other than white space or '%'). This character must exactly match the next character of input.

• A conversion specification, which commences with a '%' (percent) character. A sequence of characters from the input is converted according to this specification, and the result is placed in the corresponding pointer argument. If the next item of input does not match the conversion specification, the conversion fails-this is a matching failure.
```

So I tried implementing this in an own little program to test the behaviour.

![Testprogram](/images/compiled/Testprogram.png)

The example shows that only the literal prefix in the beginning has to be matched, everything else will be handled in the conversion and is put into the buffer.

![Flag](/images/compiled/Flag.png)