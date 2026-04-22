---
layout: post
title: "CTF-Writeup: THM - c4ptur3-th3-fl4g"
date: 2026-04-22 18:30:00 +0100
url: https://tryhackme.com/room/c4ptur3th3fl4g
difficulty: easy
author: me
tags: CTF
---

This challenge consists of different translation & shifting tasks, spectograms, steganography and file investigation.

## Translation & Shifting

For these tasks I used [CyberChef](https://gchq.github.io/CyberChef/) as reliable tool for decoding layered encodings.

There were some easy phrases using base32, base64, morse, etc.

The last one was a bit tricky, because it had multiple nested transformations with decimal, ROT47, binary, morse and base64. By carefully layering the decoders in reverse order, the final plaintext flag was recovered.

## Spectogram

A short 2-second `.wav` file was provided. Feeding this into a spectrum analyzer such as [Spek](https://www.spek.cc/) reveals the hidden message visible in the frequency domain.

![Spectogram](/images/c4ptur3th3fl4g/spectogram.png)

## Steganography

For this task a picture with spaghetti and dinosaur was provided.

First I used `strings` to look for anything hidden, but it did not reveal any hidden data. 

There was also nothing hidden in the metadata.

![Exiftool](/images/c4ptur3th3fl4g/Exiftool.png)

Then I used [Steghide](https://steghide.sourceforge.net/) to find data within the image and it gave me the hidden flag.

![Steghide](/images/c4ptur3th3fl4g/Steghide.png)

## Security through obscurity

For the last task there was again a picture to analyze. Exiftool again had nothing to show. Also Steghide yielded no results without a given passphrase. Therefore I wanted to quickly have a look at the strings.

Well and there were the answers, hidden at the end of the binary code.

![Strings](/images/c4ptur3th3fl4g/Strings.png)

