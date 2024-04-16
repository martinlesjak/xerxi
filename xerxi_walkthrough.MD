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
   ![log1php](https://github.com/martinlesjak/xerxi/blob/images/log1php.png)
   5.1 Acquiring username and password hash as the terminal loads, we set to crack the password. The password is hashed by MD5.
   ![hackerhint](https://github.com/martinlesjak/xerxi/blob/images/hackerhint.png)

6. We crack the password using a website, since johntheripper doesn't yield any results. The website: `https://www.md5online.org/md5-decrypt.html` cracks the password, throwing `ilikecats` back.
   ![ilikecats](https://github.com/martinlesjak/xerxi/blob/images/ilikecats.png)

6.1 Trying the password on login page on `eth0:80`, the user doesn't exist. But here's another page, using port 8080, which is used for websites aswell. We find something interesting.
![webapp](https://github.com/martinlesjak/xerxi/blob/images/webapp.png)

7. We try to login through the page on port 8080 with credentials acquired.
   7.1 As we can see, the login with user:`PVT` and password:`ilikecats` is successful.
   ![loginsuccess](https://github.com/martinlesjak/xerxi/blob/images/loginsuccess.png)
   7.2 A dashboard open's infront of us. It has few interactable items such as taskbar, Divison, Settings and Logout.
   ![dashboard](https://github.com/martinlesjak/xerxi/blob/images/dashboard.png)
   7.3 Upon inspecting settings, we find something interesting.
   ![settings](https://github.com/martinlesjak/xerxi/blob/images/settings.png)
   7.4 The settings panel has user, which is autocompleted by current logged user and it prompts us to write in current password and new password. Testing it, we come to a hypothesis - maybe the session saved a variable username and password aswell - it would be extremely insecure, thats for sure, but let's try. The highest privilege is GEN username. The sql sentence might look something like this: `sql="UPDATE users SET password = $password WHERE user=$user"`
   ![settingssol](https://github.com/martinlesjak/xerxi/blob/images/settingssol.png)

8. Changing the password, we try to login as GEN. It works, and we are presented with a more advanced looking dashboard.
   ![advanceddashboard](https://github.com/martinlesjak/xerxi/blob/images/advanceddashboard.png)
   8.1 After inspecting everything, Logs has an interesting entry. Two, actually. The Logs section seems to write all the changes in the system, with last being Log 7 - mysql database password update "quack". Log 6 tells us SRG is superadmin, which tells us something is not right. Second port was port 3306, which is often used for mysql.
   ![logs](https://github.com/martinlesjak/xerxi/blob/images/logs.png)
   8.2 We can try login as SRG - using same method as GEN. But unfortunately, access is denied.
   ![accessdenied](https://github.com/martinlesjak/xerxi/blob/images/accessdenied.png)

9. One option is to look for password in database. We got the password - it's `quack`. We login via this command line - `mysql -h <eth0 ip> -u root -p`. It's a success!
   ![mysqllogin](https://github.com/martinlesjak/xerxi/blob/images/mysqllogin.png)
   9.1 We can navigate mysql using commands displayed on this photo.
   ![navigation](https://github.com/martinlesjak/xerxi/blob/images/navigation.png)
   9.2 We found the password!
   ![srgpassword](https://github.com/martinlesjak/xerxi/blob/images/srgpassword.png)

10. Using MD5 tool, we decrypt SRG's password.

11. When logging into SRG's profile, we can find flag under `Personal Notes`.

We've won! Congrats. :)
