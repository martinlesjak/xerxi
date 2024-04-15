# Basics Intro
This walkthrough will cover how to hack into the challenge and not how to set it up. I'll release the file covering how to setup Docker to start the challenge.
The **Challenge's IP** is under ``ip a`` command 'eth0'.
# Docker tutorial
Coming soon.
# Challenge Walkthrough
1. We preform an NMAP scan, which reveals 3 ports open.
![loading_mainsite](url)
2. Port 80 is usually used for HTTP, so we go check it out.
![loading_mainsite](https://github.com/martinlesjak/xerxi/blob/images/first.png)
2.5 We find nothing of importance upon signing in into as Guest.
![loading_mainsite](url)
3. Trying combinations as 'user', 'admin' and 'root' as password and username, we manage to login via 'root' as username and password.
![loading_mainsite](url)
3.1 Upon loading into the page, we discover nothing of importance - a page with 'Work in Progress' in the middle.
3.2 Interestingly, the website has an interesting directory named 'wip'. We can check out if there are any other directories using either Dirbuster or Gobuster. We'll be using Gobuster via Kali Linux terminal.
![loading_mainsite](url)
