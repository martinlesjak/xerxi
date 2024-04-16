# Basics Intro

This walkthrough will cover how to hack into the challenge and not how to set it up. I'll release the file covering how to set up Docker to start the challenge. The **Challenge's IP** is under the `ip a` command 'eth0'.

# Docker Tutorial

Coming soon.

# Challenge Walkthrough

### NMAP

1. We perform an NMAP scan, which reveals 3 open ports.
   ![nmapscan](https://github.com/martinlesjak/xerxi/blob/images/nmapscan.png)

### WEBSITE

2. Port 80 is usually used for HTTP, so we go check it out.
   ![loading_mainsite](https://github.com/martinlesjak/xerxi/blob/images/first.png)

2.5. We find nothing of importance upon signing in as Guest.
   ![guest](https://github.com/martinlesjak/xerxi/blob/images/nothingofimportance.png)

3. Trying combinations like 'user', 'admin', and 'root' as username and password, we manage to login as 'root'.
   ![loginasroot](https://github.com/martinlesjak/xerxi/blob/images/loginasroot.png)

3.1. Upon loading into the page, we discover nothing of importance - a page with 'Work in Progress' in the middle.

3.2. Interestingly, the website has an interesting directory named 'wip'. We can check out if there are any other directories using either Dirbuster or Gobuster. We'll be using Gobuster via Kali Linux terminal.
   ![intdirs](https://github.com/martinlesjak/xerxi/blob/images/interestingdirs.png)

4. Using Gobuster, we can find some interesting directories. Mainsite and dashboard don't promise anything of importance, since the test and wip look more promising.
   ![gobuster](https://github.com/martinlesjak/xerxi/blob/images/gobuster.png)

4.1. Through looking in the directories, we find something of value in `/test`, named log1.php.
   ![log1find](https://github.com/martinlesjak/xerxi/blob/images/log1find.png)

5. Opening `http://your_eth0/test/log1.php`, we find something interesting.
   ![log1php](https://github.com/martinlesjak/xerxi/blob/images/log1find.png)
5.1 Acquiring username and password hash as the terminal loads, we set to crack the password. The password is hashed by MD5.
   ![log1find](https://github.com/martinlesjak/xerxi/blob/images/log1find.png)

6. We crack the password using a website, since johntheripper doesn't yield any results. The website: `https://www.md5online.org/md5-decrypt.html` cracks the password, throwing `ilikecats` back.
   ![ilikecats](https://github.com/martinlesjak/xerxi/blob/images/log1find.png)
