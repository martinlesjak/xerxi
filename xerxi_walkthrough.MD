# Basics Intro
This walkthrough will cover how to hack into the challenge and not how to set it up. I'll release the file covering how to setup Docker to start the challenge.
The **Challenge's IP** is under ``ip a`` command 'eth0'.
# Docker tutorial
Coming soon.
# Challenge Walkthrough
### NMAP
1. We preform an NMAP scan, which reveals 3 ports open.
![nmapscan](https://github.com/martinlesjak/xerxi/blob/images/nmapscan.png)
### WEBSITE
2. Port 80 is usually used for HTTP, so we go check it out.
![loading_mainsite](https://github.com/martinlesjak/xerxi/blob/images/first.png)
2.5 We find nothing of importance upon signing in into as Guest.
![guest](https://github.com/martinlesjak/xerxi/blob/images/nothingofimportance.png)
3. Trying combinations as 'user', 'admin' and 'root' as password and username, we manage to login via 'root' as username and password.
![loginasroot](https://github.com/martinlesjak/xerxi/blob/images/loginasroot.png)
3.1 Upon loading into the page, we discover nothing of importance - a page with 'Work in Progress' in the middle.
3.2 Interestingly, the website has an interesting directory named 'wip'. We can check out if there are any other directories using either Dirbuster or Gobuster. We'll be using Gobuster via Kali Linux terminal.
![intdirs](https://github.com/martinlesjak/xerxi/blob/images/interestingdirs.png)
4. Using Gobuster, we can find some interesting directories. Mainsite and dashboard don't promise anything of importance, since the test and wip look more promising.
![gobuster](https://github.com/martinlesjak/xerxi/blob/images/gobuster.png)
4.1 Through looking the directories, we find something of value in ``/test``, named log1.php.
![log1find](https://github.com/martinlesjak/xerxi/blob/images/log1find.png)

