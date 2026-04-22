---
layout: post
title: "CTF-Writeup: THM - The Game"
date: 2026-04-22 15:30:00 +0100
url: https://tryhackme.com/room/hfb1thegame
difficulty: easy
author: me
tags: CTF
---

The challenge was to analyze a Tetris-like game and recover a hidden flag from the binary.

After downloading and extracting the provided files, I ran the executable. It turnes out to be a small but polished clone of the classic Tetris game. After briefly playing it, I moved on to analyzing the binary.

![TETRIM](/images/hfb1thegame/Tetrim.png)

To begin the investigation, I opened the `.exe` file using [HxD](https://mh-nexus.de/de/hxd/) to inspect its raw contents.

![Hexcode](/images/hfb1thegame/Hexcode.png)

Since TryHackMe flags typically follow the format `THM{...}`, I searched the binary for the string `THM{`. This quickly produced a match, revealing the flag directly in the file.

![StringSearch](/images/hfb1thegame/StringSearch.png)
![Flag](/images/hfb1thegame/Flag.png)

This indicated that the flag was stored in plaintext within the binary, making it possible to retrieve it without deeper reverse engineering.
