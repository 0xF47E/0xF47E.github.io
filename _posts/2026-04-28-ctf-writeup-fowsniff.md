---
layout: post
title: "CTF-Writeup: THM - Fowsniff CTF"
date: 2026-04-28 20:30:00 +0100
url: https://tryhackme.com/room/ctf
difficulty: easy
author: me
tags: CTF
---

"This boot2root machine is brilliant for new starters. You will have to enumerate this machine by finding open ports, do some online research (its amazing how much information Google can find for you), decoding hashes, brute forcing a pop3 login and much more!

This will be structured to go through what you need to do, step by step. Make sure you are connected to our network

Credit to berzerk0(opens in new tab) for creating this machine."

I started off with scanning the target with Nmap.

![Nmap](/images/fowsniff/01nmap-scan.png)

The server exposed 4 open ports. So I started looking at the webpage on port 80.

![Browser](/images/fowsniff/02browser.png)

The creator of the challenge gave a tip to look in the web. So shortly after I found leaked password hashes for mail accounts of the company's employes.

![Leaked](/images/fowsniff/03leaked.png)

After using [John the Ripper](https://github.com/openwall/john) to crack the MD5 hashes, I had a bunch of usernames and passwords.

![Passwords](/images/fowsniff/04passwords.png)

With that I managed to get into the POP3 Mail Server. I have used msfconsole, but rather ineffective in the end, because I did not match the users with their passwords.

![Msfconsole](/images/fowsniff/05msfconsole.png)

![POP3](/images/fowsniff/06pop.png)

In the mails I found the ssh key. But it did not work with the same username I used to log into POP3. Therefore I used Hydra to bruteforce the entry.

```bash
hydra -L users.txt -p <password> ssh://ip
```

With that I managed to get access to the server via ssh.

![SSH](/images/fowsniff/07ssh.png)

The challenge gave a hint on where to look for vectors for privilege escalation.
I look for binaries the "users" group could execute.

![users](/images/fowsniff/08users.png)

The `cube.sh` posed an excellent vector for privilege escalation as it is the banner for logging into the shell. 

![cube](/images/fowsniff/09cube.png)

The script gets called by root when crafting the banner. And it was also writable for the users group. Therefore I planted a python reverse shell into the script.

![banner](/images/fowsniff/10banner.png)

On my attacking machine I started a listener for the imcoming connection.

![nc](/images/fowsniff/11nc.png)

After this was done, it was only a matter of logging in again into ssh once more.

![root](/images/fowsniff/12root.png)
