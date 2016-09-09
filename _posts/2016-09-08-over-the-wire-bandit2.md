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

### Level 11 > 12:

```console
bandit11@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  data.txt
bandit11@melinda:~$ cat data.txt
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
bandit11@melinda:~$ echo Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh | tr [a-zA-Z] [n-za-mN-ZA-M]
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

### Level 12 > 13:

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
Please note! That we must remove the created directory after we are done. So we do the following...

```console
bandit12@melinda:/tmp/jhalon$ cd ..
bandit12@melinda:/tmp$ rm -rf jhalon
bandit12@melinda:/tmp$ reset
```

### Level 13 > 14:

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

### Level 14 > 15:

```console
bandit14@melinda:~$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

### Level 15 > 16:

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

### Level 16 > 17:

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

bandit16@melinda:~$ mkdir /tmp/jhalon
bandit16@melinda:~$ cd /tmp/jhalon
bandit16@melinda:/tmp/jhalon$ nano sshkey.private
bandit16@melinda:/tmp/jhalon$ chmod 600 sshkey.private
bandit16@melinda:/tmp/jhalon$ ssh -i ./sshkey.private bandit17@localhost

```

### Level 17 > 18:

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

### Level 18 > 19:

```console
ssh bandit18@bandit.labs.overthewire.org "bash --norc"
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

### Level 19 > 20:

```console
bandit19@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  bandit20-do
bandit19@melinda:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
bandit19@melinda:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

### Level 20 > 21:

```console
bandit20@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  suconnect
bandit20@melinda:~$ nc -l 32123 < /etc/bandit_pass/bandit20
```
Open another Terminal and login to Bandit20 via `SSH`
```console
bandit20@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  suconnect
bandit20@melinda:~$ ./suconnect 32123
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
```
Now if you look back at the first terminal you will see the password
```console
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```

### Level 21 > 22:

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

### Level 22 > 23:

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
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
bandit22@melinda:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1 
8ca319486bfbbc3663ea0fbe81326349
bandit22@melinda:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

### Level 23 > 24:

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
We thus get this Bash Script
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
Contuining on in the Terminal
```console
bandit23@melinda:/etc/cron.d$ mkdir /tmp/jhalon
bandit23@melinda:/etc/cron.d$ cd /tmp/jhalon
bandit23@melinda:/tmp/jhalon$ nano
```
Write sript
```bash
#!/bin/bash

cat /etc/bandit_pass/bandit24 > tmp/jhalon/pass
```
Save as `script.sh`. Now back in our console...
```console
bandit23@melinda:/tmp/jhalon$ chmod 777 script.sh
bandit23@melinda:/tmp/jhalon$ cp script.sh /var/spool/bandit24
bandit23@melinda:/tmp/jhalon$ dir -a
.  ..  pass  script.sh
bandit23@melinda:/tmp/jhalon$ cat /tmp/jhalon/pass
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

### Level 24 > 25:

```console
bandit24@melinda:~$ mkdir /tmp/jhalon
bandit24@melinda:~$ cd /tmp/jhalon
bandit24@melinda:/tmp/jhalon$ nano
```
Write Script
```bash
#!/bin/bash
passwd="UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ"

for a in {0..9}{0..9}{0..9}{0..9}
do
    echo $passwd' '$a | nc localhost 30002 >> result &
done
```
Save as `script.sh` go back to console
```console
bandit24@melinda:/tmp/jhalon$ chmod 755 script.sh
bandit24@melinda:/tmp/jhalon$ ./script.sh
bandit24@melinda:/tmp/jhalon$ sort result | uniq -u

Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
```

### Level 25 > 26:

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
Once there, press V and it should taek you to VIM, then typr
```console
:r /etc/bandit_pass/bandit26
```
Press Enter, and you should get the password!
```console
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
```
