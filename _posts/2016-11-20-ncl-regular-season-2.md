---
layout: single
title: "NCL CTF - Regular Season: WiFi Cracking & Exploitation"
header:
  teaser: oth.png
  overlay_image: nebula.jpg
  caption: "[__NCL__](http://www.nationalcyberleague.org/)"
related: true
comments: true
---

Welcome back to part 2 of my NCL Regular Season posts. This post will cover the WiFi Cracking and Exploitation parts of the CTF.

If you haven't read part 1: [Crypto & Log Analysis](https://jhalon.github.io/ncl-regular-season-1/) then I suggest you do so!

Without wasting more of your time, let's get to it!

## Cracking (Medium):

<a href="/images/nclp-4.png"><img src="/images/nclp-4.png"></a>

For this challenge we are provided the following file: [NCL-2016-Game2-MediumWifi.pcap](https://jhalon.github.io/download/NCL-2016-Game2-MediumWifi.pcap)

<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the SSID of the vulnerable WiFi Network?__</span>

Once we open the pcap in Wireshark, all you really have to do is click on __Wireless__ in the tool bar, and from the drop down click __WLAN Traffic__.

<a href="/images/ncl-ch-2.png"><img src="/images/ncl-ch-2.png"></a>

Once we do so, we will get a pop up with the Wireless LAN Statistics. Just look at the first line under __SSID__ for the answer.

<a href="/images/ncl-cm-1.png"><img src="/images/ncl-cm-1.png"></a>

__Answer: NCL-Secure-Legacy__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What is the BSID of the vulnerable WiFi Network?__</span>

Jast as above, look at line 1, right under __BSSID__.

<a href="/images/ncl-cm-1.png"><img src="/images/ncl-cm-1.png"></a>

__Answer: c0:4a:00:80:76:e4__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What is the MAC address of the connected client that had the most combined send/received packets?__</span>

For this answer look down the __Beacons__ and __Data Pkts__ columns. We can see that __e0:55:3d:18:0c:a8__ sent/received the most packets combined!

<a href="/images/ncl-cm-1.png"><img src="/images/ncl-cm-1.png"></a>

__Answer: e0:55:3d:18:0c:a8__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __What is the password of the vulnerable WiFi Network?__</span>

For this answer we will have to use [Aircrack-NG](https://www.aircrack-ng.org/) to be able to crack the WiFI Password. Just use the aircrack-ng command with the downloaded pcap, and it should crack the password for you!

```console
root@kali:~/Downloads# aircrack-ng NCL-2016-Game2-MediumWifi.pcap 
Opening NCL-2016-Game2-MediumWifi.pcap
Read 83449 packets.

   #  BSSID              ESSID                     Encryption

   1  C0:4A:00:80:76:E4  NCL-Secure-Legacy         WEP (14842 IVs)

Choosing first network as target.

Opening NCL-2016-Game2-MediumWifi.pcap
Attack will be restarted every 5000 captured ivs.
Starting PTW attack with 14842 ivs.

                                 Aircrack-ng 1.2 rc4


                 [00:00:01] Tested 3481 keys (got 14842 IVs)

   KB    depth   byte(vote)
    0    0/  1   6E(23040) 0D(19456) 06(18688) 1E(18432) 37(18432) 
    1    0/ 15   6F(20736) 68(20224) 3B(19968) 70(19968) 64(19712) 
    2    6/  8   AC(18944) 34(18432) 39(18432) 40(18176) 4A(18176) 
    3    0/  1   45(23552) 61(19968) 24(19200) D2(19200) 02(18944) 
    4   14/ 33   50(17920) AB(17664) B8(17664) C1(17664) F7(17664) 

                     KEY FOUND! [ 6E:6F:57:45:50 ] (ASCII: noWEP )
	Decrypted correctly: 100%

```

__Answer: noWEP__
</div>

## Cracking (Hard):

<a href="/images/nclp-5.png"><img src="/images/nclp-5.png"></a>

For this challenge we are provided the following file: [NCL-2016-Game2-HardWifi.cap](https://jhalon.github.io/download/NCL-2016-Game2-HardWifi.cap)

<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the SSID of the vulnerable WiFi Network?__</span>

Once we open the pcap in Wireshark, all you really have to do is click on __Wireless__ in the tool bar, and from the drop down click __WLAN Traffic__.

<a href="/images/ncl-ch-2.png"><img src="/images/ncl-ch-2.png"></a>

Once we do so, we will get a pop up with the Wireless LAN Statistics. Just look at the first line under __SSID__ for the answer.

<a href="/images/ncl-ch-1.png"><img src="/images/ncl-ch-1.png"></a>

__Answer: NCL-Secure__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __How many data packets were captured from the associated client?__</span>

Just look down the __Data Pkts__ column, and we will see that __33:33:00:00:00:16__ has 15 packets. If you analyze the PCAP logs, you will see that the WiFi communicated directly with that client.

<a href="/images/ncl-ch-1.png"><img src="/images/ncl-ch-1.png"></a>

__Answer: 15__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What is the password of the vulnerable WiFi Network?__</span>

Just as we have done with the previous question, we will have to run aircrack-ng. But... aircrack-ng will not have the password by default! So we will have to use a wordlist! I simply used the __rockyou__ password.

```console
root@kali:~/Downloads# aircrack-ng -w /root/rockyou.txt NCL-2016-Game2-HardWifi.cap 
Opening NCL-2016-Game2-HardWifi.cap
Read 167 packets.

   #  BSSID              ESSID                     Encryption

   1  C0:4A:00:80:76:E4  NCL-Secure                WPA (1 handshake)

Choosing first network as target.

Opening NCL-2016-Game2-HardWifi.cap
Reading packets, please wait...

                                 Aircrack-ng 1.2 rc4

      [00:00:05] 19972/9822768 keys tested (3487.18 k/s) 

      Time left: 46 minutes, 51 seconds                          0.20%

                           KEY FOUND! [ 1drummer ]


      Master Key     : 36 B2 B8 EB F1 B6 0C C0 70 0B D1 56 DC 2D 13 DF 
                       A4 D7 61 6D AC C8 6C 27 A4 3D F2 E6 AC D0 42 F0 

      Transient Key  : 62 68 62 6B FB AF 21 69 02 A1 B1 B3 D7 1E A6 41 
                       31 A5 AD 5F E8 A7 E9 F6 45 B1 31 16 E6 5A A5 B9 
                       51 45 94 E0 D2 DE 13 AC D4 6E 9E 72 35 82 29 C8 
                       76 BA 62 6D 69 A2 5B D7 88 C7 26 5F D7 F7 8F 4B 

      EAPOL HMAC     : C1 67 B9 73 EE EA E9 EE 1A B2 52 E7 02 58 7F BF 
```

__Answer: 1drummer__
</div>

## PyPass:

<a href="/images/nclp-6.png"><img src="/images/nclp-6.png"></a>

For this challenge we are provided the following file: [NCL-2016-Game2-pypass.pyc](https://jhalon.github.io/download/NCL-2016-Game2-pypass.pyc)

<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the hidden flag?__</span>

For this question you needed some previous experience with reverse engineering, and python. Looking at the file that is provided to us, we see the extension is __.pyc__, which is Compiled Python Code.

To be able to disassemble the compiled code we need to use the tool [uncompyle2](https://github.com/wibiti/uncompyle2) which is a Python 2.7 byte-code decompiler.

Once you install the tool, run the following command with the file provided and we should get the disassembled code.

```console
root@kali:~/Downloads# uncompyle2 NCL-2016-Game2-pypass.pyc 
# 2016.11.20 16:24:15 CST
#Embedded file name: ./pypass.py
import sys
keys = ['a',
 'b',
 'c',
 'd',
 'e',
 'f',
 'g',
 'h',
 'i',
 'j',
 'k',
 'l',
 'm',
 'n',
 'o',
 'p',
 'q',
 'r',
 's',
 't',
 'u',
 'v',
 'w',
 'x',
 'y',
 'z',
 '0',
 '1',
 '2',
 '3',
 '4',
 '5',
 '6',
 '7',
 '8',
 '9']

def main():
    if False:
        print keys[13].upper() + keys[2].upper() + keys[11].upper() + '-' + keys[27] + keys[30] + keys[32] + keys[29] + '-' + keys[21].upper() + keys[18].upper() + keys[3].upper() + keys[9].upper()


if __name__ == '__main__':
    main()
+++ okay decompyling NCL-2016-Game2-pypass.pyc 
# decompiled 1 files: 1 okay, 0 failed, 0 verify failed
# 2016.11.20 16:24:15 CST
```

Cool! Now that we have our hands on the code, we see that the program takes a letter from the list "keys" and prints it out, while converting it to upper case.

Since we have the code, all we really have to do is reverse engineer it - more like re-engineer it - to give us the answer. Let's begin by opening __gedit__ with a new file name called __pass.py__.

```console
root@kali:~/Downloads# gedit pass.py
```

Once we open our new file, let's go ahead and write the following Python code. Notice how I included __#!/usr/bin/python__, so that our Terminal will run the code with Python and avoid any errors. At the same time I removed __def main():__ from the code and just allowed Python to print the characters for us, without us having to call the __main__ function.

```python
#!/usr/bin/python

import sys
keys = ['a',
 'b',
 'c',
 'd',
 'e',
 'f',
 'g',
 'h',
 'i',
 'j',
 'k',
 'l',
 'm',
 'n',
 'o',
 'p',
 'q',
 'r',
 's',
 't',
 'u',
 'v',
 'w',
 'x',
 'y',
 'z',
 '0',
 '1',
 '2',
 '3',
 '4',
 '5',
 '6',
 '7',
 '8',
 '9']


print keys[13].upper() + keys[2].upper() + keys[11].upper() + '-' + keys[27] + keys[30] + keys[32] + keys[29] + '-' + keys[21].upper() + keys[18].upper() + keys[3].upper() + keys[9].upper()
```

Once we save that code, let's go ahead and give it executable permissions, and then run the code. We should thus get the hidden flag!

```console
root@kali:~/Downloads# chmod +x pass.py 
root@kali:~/Downloads# ./pass.py 
NCL-1463-VSDJ
```

__Answer: NCL-1463-VSDJ__
</div>

## EasySploit:

<a href="/images/nclp-7.png"><img src="/images/nclp-7.png"></a>

For this challenge we are provided the following file: [NCL-2016-Game2-EasySploit.c](https://jhalon.github.io/download/NCL-2016-Game2-EasySploit.c)

<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the gcc flag used to disable stack protection?__</span>

GCC is the [GNU Compiler Collection](https://gcc.gnu.org/) usually used for C and C++ - some understanding of those languages is needed here.

Google GCC Disable Stack PRotection > The answer is provided [here](http://stackoverflow.com/questions/2340259/how-to-turn-off-gcc-compiler-optimization-to-enable-buffer-overflow).

__Answer: fno-stack-protector__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What type of security vulnerability exists in this program?__</span>

Since this is a C file, all we really need to do is just open the file in a text editor to read the code.

```console
root@kali:~/Downloads# gedit NCL-2016-Game2-EasySploit.c 
```

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
  char buff[15];
  int pass = 0;

  printf("\n Enter the password : \n");
  gets(buff);

  if(strcmp(buff, "asecurepassword"))
  {
    printf ("\n Wrong Password \n");
  }
  else
  {
    printf ("\n Correct Password \n");
    pass = 1;
  }

  if(pass)
  {
    /* Now Give root or admin rights to user*/
    printf ("\n Root privileges given to the user \n");
  }

  return 0;
}
```

Looking at the code, we can see that it is written in C. Now two things really stand out here.

1) __char buff[15];__

2) __gets(buff);__

Let me explain to you what is occurring - for those who don't understand C language. The char (or character - used for strings) ‘buff’ represents an array of 15 bytes where buff[0] is the left boundary and buff[14] is the right boundary of the buffer.

A buffer, in terms of a program in execution, can be thought of as a region of computer’s main memory that has certain boundaries in context with the program variable that references this memory.

Since the C function [gets](https://www.tutorialspoint.com/c_standard_library/c_function_gets.htm) is being used, we instantly know that the program is insecure and a Buffer Overflow is present. This is due to the fact that __gets__ does not terminate the end of the strings buffer (or 15 chars).

A buffer is said to be overflown when the data (meant to be written into memory buffer) gets written past the left or the right boundary of the buffer. This way the data gets written to a portion of memory which does not belong to the program variable that references the buffer.

For this to be secure, we would need to use [fgets](https://www.tutorialspoint.com/c_standard_library/c_function_fgets.htm) , which terminates the end of the string buffer with a null byte '\0', that stops further execution beyond the 15 chars.

Overall, this is a [Buffer Overflow](https://en.wikipedia.org/wiki/Buffer_overflow) Vulnerability.


__Answer: Buffer Overflow__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __On what line number is a vulnerable function call made?__</span>

Like I explained above, look for the line with the unsecure __gets__ command, which is on line 10.

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
  char buff[15];
  int pass = 0;

  printf("\n Enter the password : \n");
  gets(buff);

  if(strcmp(buff, "asecurepassword"))
  {
    printf ("\n Wrong Password \n");
  }
  else
  {
    printf ("\n Correct Password \n");
    pass = 1;
  }

  if(pass)
  {
    /* Now Give root or admin rights to user*/
    printf ("\n Root privileges given to the user \n");
  }

  return 0;
}
```

__Answer: 10__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __Without entering the "correct" password, what is the minimum number of input characters needed to bypass the password check?__</span>

If you actually read my explanation in question 1, then you would know that since __gets__ is being used, and the buffer is not being terminated at 15 chars... we would have to use a minimum number of 16 chars to overrun the buffer's boundary and overwrite to adjacent memory locations.

```c
#include <stdio.h>
#include <string.h>

int main(void)
{
  char buff[15];
  int pass = 0;

  printf("\n Enter the password : \n");
  gets(buff);

  if(strcmp(buff, "asecurepassword"))
  {
    printf ("\n Wrong Password \n");
  }
  else
  {
    printf ("\n Correct Password \n");
    pass = 1;
  }

  if(pass)
  {
    /* Now Give root or admin rights to user*/
    printf ("\n Root privileges given to the user \n");
  }

  return 0;
}
```

__Answer: 16__
</div>

Thanks for reading! I hope you guys learned something from reading the NCL posts - as I myself have learned a ton!

Please stay tuned for more, including posts on the Kaizen CTF, VulnHub, and more!
