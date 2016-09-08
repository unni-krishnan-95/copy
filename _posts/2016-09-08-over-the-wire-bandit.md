---
layout: single
title: "Overthrwire: Bandit Solution 1-10"
commnets: true
---

Over the past couple weeks, I have been getting deeper and deeper into the realm of penetration testing (or as many like to call it... hacking). I have been obsessively doing research, practicing, and honing my basic level Linux skills, as well as expanding my toolset knowledge.

Just recently in my school, we created an “__Information Security Club__”, that was mainly focused on learning, and expanding student knowledge in the Information Security field, as well as introducing many to the hacking culture, and techniques. 
The club recently decided to participate in the NCL ([National Cyber League]( http://www.nationalcyberleague.org/)) which is an ongoing virtual training ground for collegiate students to develop, practice, and validate their cybersecurity skills using next-generation high-fidelity simulation environments.

The NCL is a CTF ([Capture The Flag]( https://en.wikipedia.org/wiki/Capture_the_flag#Computer_security)) based wargame where students, paired in teams or solo, compete against each other for points by exploiting security vulnerabilities. The NCL is a beginner based CTF that introduces students to the concept of CTF, and teaches them hacking techniques, vulnerabilities, exploits, etc.

During the time this club was created, I taught the students about many information security basics, and hacking terminology. Though recently, I stumbled across [overthewire.org](http://overthewire.org/wargames/), a wargaming site that allows you to practice your skills; and have been overly obsessed with it. Giving this to many of my students, and asking them to start with “__Bandit__”, I aimed to help them learn the basics of Linux and its commands.

The following below are the solutions to the first 10 levels of “__Bandit__”. Though I must state, use the following solutions to learn and compare them with your own answers, also use Google when needed!

### Level 0:

The Zero Level is pretty easy, it's there just to make sure that you can connect the the Bandit Lab. I will be using Linux for the following levels, so all of the commands I use (following after the `~#` and or `~$`) are ran under the console.

To get to level 0 we need to simply __SSH__ into Bandit wit the username: __bandit0__ and password: __bandit0__

```console
root@kali:~# ssh bandit0@bandit.labs.overthewire.org
```
Congrats! You have accessed Bandit and are in the SSH Shell!

### Level 0 -> 1:

The password for the next level is stored in a file called __readme__ located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH to log into that level and continue the game.

```console
bandit0@melinda:~$ ls
readme
bandit0@melinda:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```
Now, from here type `exit` and SSH back into th next level by running

```console
root@kali:~# ssh bandit1@bandit.labs.overthewire.org
```

Remeber, you msut SSH into the next new level, so just replace the user name before the `@` with the next level and use the password from the previous level.

### Level 1 -> 2:

The password for the next level is stored in a file called - located in the home directory

```console
bandit1@melinda:~$ ls -a
- . .. .bash_logout .bashrc .profile
bandit1@melinda:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

### Level 2 -> 3:

The password for the next level is stored in a file called __spaces in this filename__ located in the home directory

```console
bandit2@melinda:~$ dir
spaces\ in\ this\ filename
bandit1@melinda:~$ cat spaces\ in\ this\ filename
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

### Level 3 -> 4:

The password for the next level is stored in a hidden file in the __inhere__ directory.

```console
bandit3@melinda:~$ ls
inhere
bandit3@melinda:~$ cd inhere
bandit3@melissa:~/inhere$ ls -a
. .. .hidden
bandit3@melissa:~/inhere$ cat .hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

### Level 4 - >5:

The password for the next level is stored in the only human-readable file in the __inhere__ directory. Tip: if your terminal is messed up, try the “reset” command.

```console
bandit4@melinda:~$ ls -a
inhere
bandit4@melinda:~$ cd inhere
bandit4@melissa:~/inhere$ ls -la
drwxr-xr-x 2 root    root    4096 2012-05-10 23:51 .
drwxr-xr-x 3 root    root    4096 2012-05-10 23:51 ..
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file00
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file01
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file02
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file03
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file04
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file05
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file06
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file07
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file08
-rw-r----- 1 bandit5 bandit4   33 2012-05-10 23:51 -file09
bandit4@melissa:~/inhere$ file ./-*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@melissa:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

### Level 5 -> 6:

The password for the next level is stored in a file somewhere under the __inhere__ directory and has all of the following properties: - human-readable - 1033 bytes in size - not executable

```console
bandit5@melinda:~$ ls
inhere
bandit5@melinda:~$ cd inhere
bandit5@melissa:~/inhere$ ls -a
.
bandit5@melissa:~/inhere$ find -type f -size 1033c
./maybehere07/.file2
bandit5@melissa:~/inhere$ cd maybehere07
bandit5@melissa:~/inhere/maybehere07$ cat ./.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

### Level 6 -> 7:

The password for the next level is stored __somewhere on the server__ and has all of the following properties: - owned by user bandit7 - owned by group bandit6 - 33 bytes in size

```console
bandit6@melinda:~$ find / -user bandit7 -group bandit6 -size 32c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@melinda:~$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```

### Level 7 -> 8:

The password for the next level is stored in the file __data.txt__ next to the word __millionth__

```console
bandit7@melinda:~$ ls -a
. .. .bash_logout .bashrc .profile data.txt
bandit7@melinda:~$ awk '/^millionth\ {print $2;}' data.txt
cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```

### Level 8 -> 9:

The password for the next level is stored in the file __data.txt__ and is the only line of text that occurs only once

```console
bandit8@melinda:~$ ls -a
. ..
bandit8@melinda:~$ cat data.txt | sort | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

### Level 9 -> 10:

The password for the next level is stored in the file __data.txt__ in one of the few human-readable strings, beginning with several ‘=’ characters.

```console
bandit9@melinda:~$ ls -a
. ..
bandit9@melinda:~$ strings data.txt | grep "="
```

### Level 10 -> 11

The password for the next level is stored in the file __data.txt__, which contains base64 encoded data

```console
bandit10@melinda:~$ ls -a
. ..
bandit10@melinda:~$cat data.txt

bandit10@melinda:~$ echo  | base64 --decode

```
