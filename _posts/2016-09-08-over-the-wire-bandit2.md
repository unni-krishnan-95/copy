---
layout: single
title: "OverTheWire: 'Bandit' Solutions 11-25"
header:
  teaser: oth.png
  overlay_image: ZenBG.png
  caption: "[__OverTheWire__](http://overthewire.org/wargames/)"
related: true
comments: true
---

Hey, Welcome Back! This post is the continuation to the "__Bandit__" Wargame found at: [overthewire.org](http://overthewire.org/wargames/bandit/).

Today I will be covering Solutions 11 through 25, so if you haven't completed Levels 1-10 in __Bandit__ then I **highly** suggest you do so before you advance to the higher levels; since 1-10 provides you with a good basic foundation for the future levels. You can read my write-up and solutions for 1-10 [here](https://jhalon.github.io/over-the-wire-bandit1/)!

And remember folks, if you get stuck on a level... don't just look up the solution! Google the question you have, and read any of the "__Helpful Reading Materials__" posted in each level. The point of these wargames is to learn, and not just copy!

So, without further adieu... let's begin!

### Level 11 -> 12:
The password for the next level is stored in the file __data.txt__, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

```console
bandit11@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  data.txt
bandit11@melinda:~$ cat data.txt
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
bandit11@melinda:~$ echo Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh | tr [a-zA-Z] [n-za-mN-ZA-M]
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

### Level 12 -> 13:
The password for the next level is stored in the file __data.txt__, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

```console
bandit12@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  data.txt
bandit12@melinda:~$ mkdir /tmp/jhalon
bandit12@melinda:~$ xd -r data.txt > /tmp/jhalon/file.bin
bandit12@melinda:~$ cd /tmp/jhalon
bandit12@melinda:/tmp/jhalon$ ls -a
.  ..  file.bin
bandit12@melinda:/tmp/jhalon$ file file.bin
file.bin: gzip compressed data, was "data2.bin", from Unix, last modified: Fri Nov 14 10:32:20 2014, max compression
bandit12@melinda:/tmp/jhalon$ zcat file.bin | file -
/dev/stdin: bzip2 compressed data, block size = 900k
bandit12@melinda:/tmp/jhalon$ zcat file.bin | bzcat | file -
/dev/stdin: gzip compressed data, was "data4.bin", from Unix, last modified: Fri Nov 14 10:32:20 2014, max compression
bandit12@melinda:/tmp/jhalon$ zcat file.bin | bzcat | zcat | file -
/dev/stdin: POSIX tar archive (GNU)
bandit12@melinda:/tmp/jhalon$ zcat file.bin | bzcat | zcat | tar xO | file -
/dev/stdin: POSIX tar archive (GNU)
bandit12@melinda:/tmp/jhalon$ zcat file.bin | bzcat | zcat | tar xO | tar xO | file -
/dev/stdin: bzip2 compressed data, block size = 900k
bandit12@melinda:/tmp/jhalon$ zcat file.bin | bzcat | zcat | tar xO | tar xO | bzcat | file -
/dev/stdin: POSIX tar archive (GNU)
bandit12@melinda:/tmp/jhalon$ zcat file.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | file -
/dev/stdin: gzip compressed data, was "data9.bin", from Unix, last modified: Fri Nov 14 10:32:20 2014, max compression
bandit12@melinda:/tmp/jhalon$ zcat file.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat | file -
/dev/stdin: ASCII text
bandit12@melinda:/tmp/jhalon$ zcat file.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat         
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```
Please note! That we __MUST__ remove the created directory after we are done. So we do the following...

```console
bandit12@melinda:/tmp/jhalon$ cd ..
bandit12@melinda:/tmp$ rm -rf jhalon
bandit12@melinda:/tmp$ reset
```
__NOTE:__ Everytime you create a directory in __/tmp/__ from now one, delete it before moving on.

### Level 13 -> 14:
The password for the next level is stored in __/etc/bandit_pass/bandit14__ and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

```console
bandit13@melinda:~$ ls -a 
.  ..  .bash_logout  .bashrc  .profile  sshkey.private
bandit13@melinda:~$ ssh -i sshkey.private bandit14@localhost
Are you sure you want to continue connecting (yes/no)? yes
```

Great! We are inside Bandit14! So now let's get the password from __/etc/bandit_pass/bandit14__

```console
bandit14@melinda:~$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

### Level 14 -> 15:
The password for the next level can be retrieved by submitting the password of the current level to __port 30000 on localhost__.

```console
bandit14@melinda:~$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

### Level 15 -> 16:
The password for the next level can be retrieved by submitting the password of the current level to __port 30001 on localhost__ using SSL encryption.

__Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…__

```console
bandit15@melinda:~$ openssl s_client -ign_eof -connect localhost:30001
...[redacted]...
SSL-Session:
    ...[redacted]...
    Verify return code: 18 (self signed certificate)
---
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
```

### Level 16 -> 17:
The credentials for the next level can be retrieved by submitting the password of the current level to a __port on localhost in the range 31000 to 32000__. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

```console
bandit16@melinda:~$ nmap -p 31000-32000 -sV  localhost

Starting Nmap 6.40 ( http://nmap.org ) at 2016-09-09 01:39 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00050s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE VERSION
31046/tcp open  echo
31518/tcp open  msdtc   Microsoft Distributed Transaction Coordinator (error)
31691/tcp open  echo
31790/tcp open  msdtc   Microsoft Distributed Transaction Coordinator (error)
31960/tcp open  echo
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 41.34 seconds

bandit16@melinda:~$ echo cluFn7wTiGryunymYOu4RcffSxQluehd | openssl s_client -quiet -connect localhost:31518
depth=0 CN = li190-250.members.linode.com
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = li190-250.members.linode.com
verify return:1
cluFn7wTiGryunymYOu4RcffSxQluehd

bandit16@melinda:~$ echo cluFn7wTiGryunymYOu4RcffSxQluehd |openssl s_client -quiet -connect localhost:31790
depth=0 CN = li190-250.members.linode.com
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = li190-250.members.linode.com
verify return:1
Correct!
-----BEGIN RSA PRIVATE KEY-----
[redacted]
-----END RSA PRIVATE KEY-----
```

Great! So let's copy the RSA Key (Don't forget to get the Header and Footer) and create a new file in a tmp directory.

```console
bandit16@melinda:~$ mkdir /tmp/jhalon
bandit16@melinda:~$ cd /tmp/jhalon
bandit16@melinda:/tmp/jhalon$ nano sshkey.private
bandit16@melinda:/tmp/jhalon$ chmod 600 sshkey.private
bandit16@melinda:/tmp/jhalon$ ssh -i ./sshkey.private bandit17@localhost

```

### Level 17 -> 18:
There are 2 files in the homedirectory: __passwords.old__ and __passwords.new__. The password for the next level is in __passwords.new__ and is the only line that has been changed between __passwords.old__ and __passwords.new__

__NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19__

```console
bandit17@melinda:~$ ls -a
.   .bandit16.password  .bashrc   .ssh                    passwords.new
..  .bash_logout        .profile  .ssl-cert-snakeoil.key  passwords.old
bandit17@melinda:~$ diff passwords.new passwords.old
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> BS8bqB1kqkinKJjuxL6k072Qq9NRwQpR
```

__Note:__ `kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd` is our password as `diff` shows what needs to be changed to equal the second file. `<` means first file (so __passwords.new__) and `>` means second file (so __passwords.old__)

### Level 18 -> 19:
The password for the next level is stored in a file __readme__ in the homedirectory. Unfortunately, someone has modified __.bashrc__ to log you out when you log in with SSH.

```console
root@kali:~# ssh bandit18@bandit.labs.overthewire.org "bash --norc"
ls -a
.
..
.bash_logout
.bashrc
.profile
readme
cat readme
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

### Level 19 -> 20:
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used to setuid binary.

```console
bandit19@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  bandit20-do
bandit19@melinda:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
bandit19@melinda:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

### Level 20 -> 21:
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

__NOTE:__ To beat this level, you need to login twice: once to run the setuid command, and once to start a network daemon to which the setuid will connect.

__NOTE 2:__ Try connecting to your own network daemon to see if it works as you think

```console
bandit20@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  suconnect
bandit20@melinda:~$ nc -l 32123 < /etc/bandit_pass/bandit20
```
Once you got NC (Netcat) listening on port 32123 (or any port of your choosing), open another Terminal and login to Bandit20 via SSH.

```console
bandit20@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  suconnect
bandit20@melinda:~$ ./suconnect 32123
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
```

Now if you look back at the first terminal you will see the password!

```console
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```

### Level 21 -> 22:
A program is running automatically at regular intervals from __cron__, the time-based job scheduler. Look in __/etc/cron.d/__ for the configuration and see what command is being executed.

```console
bandit21@melinda:~$ cd /etc/cron.d/
bandit21@melinda:/etc/cron.d$ ls -a
.                  cronjob_bandit24       natas25_cleanup   semtex0-ppc
..                 cronjob_bandit24_root  natas25_cleanup~  semtex5
.placeholder       leviathan5_cleanup     natas26_cleanup   sysstat
behemoth4_cleanup  manpage3_resetpw_job   natas27_cleanup   vortex0
cron-apt           melinda-stats          php5              vortex20
cronjob_bandit22   natas-session-toucher  semtex0-32
cronjob_bandit23   natas-stats            semtex0-64
bandit21@melinda:/etc/cron.d$ cat cronjob_bandit22
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@melinda:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@melinda:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI

```

### Level 22 -> 23:
A program is running automatically at regular intervals from __cron__, the time-based job scheduler. Look in __/etc/cron.d/__ for the configuration and see what command is being executed.

__NOTE:__ Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

```console
bandit22@melinda:~$ cd /etc/cron.d/
bandit22@melinda:/etc/cron.d$ ls -a
.                  cronjob_bandit24       natas25_cleanup   semtex0-ppc
..                 cronjob_bandit24_root  natas25_cleanup~  semtex5
.placeholder       leviathan5_cleanup     natas26_cleanup   sysstat
behemoth4_cleanup  manpage3_resetpw_job   natas27_cleanup   vortex0
cron-apt           melinda-stats          php5              vortex20
cronjob_bandit22   natas-session-toucher  semtex0-32
cronjob_bandit23   natas-stats            semtex0-64
bandit22@melinda:/etc/cron.d$ cat cronjob_bandit23
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@melinda:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
```

Running cat on __/usr/bin/cronjob_bandit23.sh__ we get the following Bash Script

```bash
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

From here, we will go ahead and try to find what the MD5 Check Sum of the echo is, following the `cut` pipe.

```
bandit22@melinda:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1 
8ca319486bfbbc3663ea0fbe81326349
bandit22@melinda:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

### Level 23 -> 24:
A program is running automatically at regular intervals from __cron__, the time-based job scheduler. Look in __/etc/cron.d/__ for the configuration and see what command is being executed.

__NOTE:__ This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

__NOTE 2:__ Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

```console
bandit22@melinda:~$ cd /etc/cron.d/
bandit23@melinda:/etc/cron.d$ ls -a
.                  cronjob_bandit24       natas25_cleanup   semtex0-ppc
..                 cronjob_bandit24_root  natas25_cleanup~  semtex5
.placeholder       leviathan5_cleanup     natas26_cleanup   sysstat
behemoth4_cleanup  manpage3_resetpw_job   natas27_cleanup   vortex0
cron-apt           melinda-stats          php5              vortex20
cronjob_bandit22   natas-session-toucher  semtex0-32
cronjob_bandit23   natas-stats            semtex0-64
bandit23@melinda:/etc/cron.d$ cat cronjob_bandit24
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@melinda:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
```

Opening the __cronjob_bandit24.sh__ script we get the following Bash Script, seen below:

```bash
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
	echo "Handling $i"
	timeout -s 9 60 "./$i"
	rm -f "./$i"
    fi
done
```

We will go ahead and create a temporary directory.

```console
bandit23@melinda:/etc/cron.d$ mkdir /tmp/jhalon
bandit23@melinda:/etc/cron.d$ cd /tmp/jhalon
bandit23@melinda:/tmp/jhalon$ nano
```

Once you open __Nano__ we will go ahead and write our own script to inject.

```bash
#!/bin/bash

cat /etc/bandit_pass/bandit24 > tmp/jhalon/pass
```

Save this new script as `script.sh`. And go back into our console...

```console
bandit23@melinda:/tmp/jhalon$ chmod 777 script.sh
bandit23@melinda:/tmp/jhalon$ cp script.sh /var/spool/bandit24
bandit23@melinda:/tmp/jhalon$ dir -a
.  ..  pass  script.sh
bandit23@melinda:/tmp/jhalon$ cat /tmp/jhalon/pass
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

### Level 24 -> 25:
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

```console
bandit24@melinda:~$ mkdir /tmp/jhalon
bandit24@melinda:~$ cd /tmp/jhalon
bandit24@melinda:/tmp/jhalon$ nano
```

We will goahead and write a new Bash Script to Brute Force the PIN while attempting a connection.

```bash
#!/bin/bash
passwd="UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ"

for a in {0-10000}
do
    echo $passwd' '$a | nc localhost 30002 >> result &
done
```

Save the script as `script.sh`, and go back to console to run the script.

```console
bandit24@melinda:/tmp/jhalon$ chmod 755 script.sh
bandit24@melinda:/tmp/jhalon$ ./script.sh
bandit24@melinda:/tmp/jhalon$ sort result | uniq -u

Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
```

### Level 25 -> 26:
Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not __/bin/bash__, but something else. Find out what it is, how it works and how to break out of it.

```console
bandit25@melinda:~$ ls -a
.   .bandit24.password  .bashrc  .profile
..  .bash_logout        .pin     bandit26.sshkey
bandit25@melinda:~$ cat /etc/passwd | grep bandit26 
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
bandit25@melinda:~$ cat /usr/bin/showtext 
#!/bin/sh

more ~/text.txt
exit 0
```

Before we try to SSH into bandit26, shrink the Console down to only 5 lines and run the `SSH` command.

```console
bandit25@melinda:~$ ssh -i bandit26.sshkey bandit26@localhost
```

Once the command is ran, press V and it should take you to VIM, then type:

```console
:r /etc/bandit_pass/bandit26
```

Press Enter, and you should get the password!

```console
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
```
