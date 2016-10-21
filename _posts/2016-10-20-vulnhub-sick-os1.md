---
layout: single
title: "VulnHub 'SickOS: 1.1' - CTF"
header:
  teaser: oth.png
  overlay_image: so-banner.jpg
  caption: "[__VulnHub__](https://www.vulnhub.com/entry/sickos-11,132/)"
related: true
comments: true
---

Welcome back to another VulnHub CTF write-up! Today we will be pwning SickOS 1.1 - which can be found here on [VulnHub](https://www.vulnhub.com/entry/sickos-11,132/).

The VulnHub VM's have so far been an amazing experience for me, as they provided me with a ton of new material to expand on. I've gained a deeper insight on hacking methodologies, the [Penetration Testing Execution Standard](http://www.pentest-standard.org/index.php/Main_Page), and new vulnerabilities, as well as attack vectors.

If this is the first time you are visiting my page (welcome!) and want to read more VulnHub write-ups then you can follow the links below to read more about the Mr. Robot VM, and the Stapler VM!

<ul>
<li><a href="https://jhalon.github.io/vulnhub-mr-robot1/">Mr.Robot - CTF</a></li>
<li><a href="https://jhalon.github.io/vulnhub-stapler1/">Stapler 1 - CTF</a></li>
</ul>

Before we jump into this VM I just want to point out that this VM was created to be simillar to what you can experience on the [OSCP](https://www.offensive-security.com/information-security-certifications/oscp-offensive-security-certified-professional/) labs, so I took that into consideration when pwning SickOS. I avoided using Metasploit - since the OSCP Exam states that you can't really use it, plus not using metasploit teaches you how to do explotation manually. You can read more about the OSCP Exam [here](https://support.offensive-security.com/#!oscp-exam-guide.md).

Alright, I'm eager to take down SickOS - so let's get to it!

## Description

Name........: SickOs1.1
Date Release: 11 Dec 2015
Author......: D4rk
Series......: SickOs
Objective...: Get /root/a0216ea4d51874464078c618298b1367.txt

This CTF gives a clear analogy how hacking strategies can be performed on a network to compromise it in a safe environment. The vm is very similar to labs faced in OSCP. The objective is to compromise the network/machine and gain Administrative/root privileges on them.

## The Hack

As always, let's start by usng `netstat` to find out what computers on our network, so we can pinpoint the target.

```console
 Currently scanning: 192.168.29.0/16   |   Screen View: Unique Hosts           
                                                                               
 6 Captured ARP Req/Rep packets, from 6 hosts.   Total size: 360               
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.1.1     -----redacted----      1      60  NETGEAR                     
 192.168.1.2     -----redacted----      1      60  Micro-Star INTL CO., LTD.   
 192.168.1.6     -----redacted----      1      60  Dell Inc.                   
 192.168.1.9     00:0c:29:5b:b2:25      1      60  VMware, Inc. 
```

Our attack target will be **192.168.1.9**. Once we pinpointed our attack target, let's go ahead and fingerprint the machine by running an nmap scan agasint it.

```console
Starting Nmap 7.25BETA2 ( https://nmap.org ) at 2016-10-15 16:11 CDT
Nmap scan report for 192.168.1.9
Host is up (0.00083s latency).
Not shown: 997 filtered ports
PORT     STATE  SERVICE    VERSION
22/tcp   open   ssh        OpenSSH 5.9p1 Debian 5ubuntu1.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 09:3d:29:a0:da:48:14:c1:65:14:1e:6a:6c:37:04:09 (DSA)
|   2048 84:63:e9:a8:8e:99:33:48:db:f6:d5:81:ab:f2:08:ec (RSA)
|_  256 51:f6:eb:09:f6:b3:e6:91:ae:36:37:0c:c8:ee:34:27 (ECDSA)
3128/tcp open   http-proxy Squid http proxy 3.1.19
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported: GET HEAD
|_http-server-header: squid/3.1.19
|_http-title: ERROR: The requested URL could not be retrieved
8080/tcp closed http-proxy
MAC Address: 00:0C:29:5B:B2:25 (VMware)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.11 - 4.1
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.83 ms 192.168.1.9

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.78 seconds
```
