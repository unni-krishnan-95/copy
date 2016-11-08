---
layout: single
title: "NCL CTF - Preseason: Network Traffic Analysis (Part 1)"
header:
  teaser: oth.png
  overlay_image: nebula.jpg
  caption: "[__NCL__](http://www.nationalcyberleague.org/)"
related: true
comments: true
---

Welcome back to the continuation of the NCL Preseason Posts! Today we will be covering __Part 1__ of the __Network Traffic Analysis__ portion of the NCL Preseason game. If you don't know what the NCL is, or what these posts are about, then I suggest you go back and read my Introduction Post which can be found [here](https://jhalon.github.io/ncl-intro-osint/)!

Also, if you missed my previous write-ups for the preseason, you can find the Cryptography portion [here](https://jhalon.github.io/ncl-crypto/) and the Log Analysis portion [here](https://jhalon.github.io/ncl-log-analysis/)!

Just a fair warning that this post will be fairly long and will be broken down into 2 parts - so let's strap in, and get to it!

## FTP

<a href="/images/ncl11.png"><img src="/images/ncl11.png"></a>

For this challenge we are provided the following file: [NCL-2016-Pre-FTP.pcap](https://jhalon.github.io/download/NCL-2016-Pre-FTP.pcap)

<a href="/images/sql3.png"><img src="/images/sql3.png"></a>

<div class="rBorder" markdown="1">
<span style="color:red">1. __What was the first username/password combination attempt made to log in to the server? e.g. 'user/password'__</span>

When we open up our pcap in Wireshark, the first thing we want to do is follow the __TCP stream__ of the first packet in the capture. Once we do, we are provided with the following stream information and the corresponding username/password.

<a href="/images/ncl-ftp1.png"><img src="/images/ncl-ftp1.png"></a>

__Answer: user1/cyberskyline__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What software is the FTP server running? (Include name and version)__</span>

Since we are already in the TCP stream view, we can see the first line is the server’s banner information, this provides us the server and it's version.

<a href="/images/ncl-ftp1.png"><img src="/images/ncl-ftp1.png"></a>

__Answer: FileZilla 0.9.53__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What is the first username/password combination that allows for successful authentication?__</span>

In our TCP stream view, we can go up to the next stream and we will be presented with annother login attempt.

<a href="/images/ncl-ftp2.png"><img src="/images/ncl-ftp2.png"></a>

__Answer: user1/metropolis__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __What is the first command the user executes on the ftp server?__</span>

Looking at the stream, and understanding FTP commands we can rule out __PORT__ as a legit command, so we are left with __LIST__.

<a href="/images/ncl-ftp2.png"><img src="/images/ncl-ftp2.png"></a>

__Answer: LIST__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __What file is deleted from the ftp server"?__</span>

The __DELE__ command is being used, which deletes a specified file on the server. That file is our answer.

<a href="/images/ncl-ftp2.png"><img src="/images/ncl-ftp2.png"></a>

__Answer: bank.cap__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __What file is uploaded to the ftp server?__</span>

The __STOR__ command allows you to uplaod files to an FTP server. THe file name after the command is our answer.

<a href="/images/ncl-ftp2.png"><img src="/images/ncl-ftp2.png"></a>

__Answer: compcodes.zip__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">7. __What is the MD5 sum of the uploaded file?__</span>

To do this we have to increment our TPC stream till we find the __FTP-DATA__ of the file being uploaded. We find the data in stream 6. TO get the MD5 sum of the file, we have to change the __Show data as__ to __RAW__ as shown below. Once done, go ahead and save that file to the root directory. 

<a href="/images/ncl-ftp3.png"><img src="/images/ncl-ftp3.png"></a>

Once the file is saved, we will use the __md5sum__ command in Linux to give us the file's MD5 Hash.

```console
root@kali:~# ls
Desktop    download   hashcat  node-v0.4.4  Public     Videos
Documents  Downloads  Music    Pictures     Templates
root@kali:~# md5sum download
3303628e25d43be4e11cc8878c5c5878  download
```

__Answer: 3303628e25d43be4e11cc8878c5c5878__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">8. __What file does the anonymous user download?__</span>

Once again, back in the TPC stream, at stream 4 - we see that someone is logging in as anonymous. The file name that we need for our answer is used with the __RETR__ command.

<a href="/images/ncl-ftp4.png"><img src="/images/ncl-ftp4.png"></a>

__Answer: compcodes.zip__
</div>

## DNS

<a href="/images/ncl12.png"><img src="/images/ncl12.png"></a>

For this challenge we are provided the following file: [NCL-2016-Pre-DNS.cap](https://jhalon.github.io/download/NCL-2016-Pre-DNS.cap)

<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the type of the DNS record requested?__</span>

Simply type in __dns__ in the Wireshark filter to leave us only with the DNS packets. The first query will be our answer.

<a href="/images/ncl-dns1.png"><img src="/images/ncl-dns1.png"></a>

__Answer: AXFR__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What domain was requested?__</span>

Looking at the AXFR query we see the domain name as well.

<a href="/images/ncl-dns1.png"><img src="/images/ncl-dns1.png"></a>

__Answer: etas.com__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __How many items were in the response?__</span>

Click on the 2nd dns packet which will be our response, and dig into the __Answers__ section.

<a href="/images/ncl-dns2.png"><img src="/images/ncl-dns2.png"></a>

__Answer: 4__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __What is the TTL for all of the records?__</span>

Dig into on of the answers, and look for the __Time to live__.

<a href="/images/ncl-dns3.png"><img src="/images/ncl-dns3.png"></a>

__Answer: 3600__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __What is the IP address for the "welcome" subdomain?__</span>

Looking back at the answers for __welcome.etas.com__ it gives us the IP address.

<a href="/images/ncl-dns3.png"><img src="/images/ncl-dns3.png"></a>

__Answer: 1.1.1.1__
</div>

## HTTP 1

<a href="/images/ncl13.png"><img src="/images/ncl13.png"></a>

For this challenge we are provided the following file: [NCL-2016-Pre-HTTP 1.cap](https://jhalon.github.io/download/NCL-2016-Pre-HTTP 1.cap)

<div class="rBorder" markdown="1">
<span style="color:red">1. __What Linux tool was used to execute a file download?__</span>

As we have done before, follow the TCP stream of the first packet and you should see the __User-Agent__, which is what initiated the request. We see that the Linux tool __wget__ was used.

<a href="/images/ncl-http1-1.png"><img src="/images/ncl-http1-1.png"></a>

__Answer: wget__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What is the name of the web server software that handled the request?__</span>

Just look for the __Server__ line for the answer.

<a href="/images/ncl-http1-1.png"><img src="/images/ncl-http1-1.png"></a>

__Answer: Nginx__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __From what IP address did the request originate?__</span>

Going back to our packets, let's fine the __GET__ command and look at __Source__.

<a href="/images/ncl-http1-2.png"><img src="/images/ncl-http1-2.png"></a>

__Answer: 192.168.1.140__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __What is the IP address of the server?__</span>

Same packet, just look at __Destination__.

<a href="/images/ncl-http1-2.png"><img src="/images/ncl-http1-2.png"></a>

__Answer: 174.143.213.184__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __What is the md5sum of the file downloaded?__</span>

For this one, we have to go to __File__ > __Export Objects__ > __HTTP__ and you will see a pop up like below.

<a href="/images/ncl-http1-3.png"><img src="/images/ncl-http1-3.png"></a>

Go ahead and save that image to the root directory, and let's run the __md5sum__ command against the image to the get MD5 Hash.

```console
root@kali:~# ls
Desktop    download   hashcat   Music        Pictures  Templates
Documents  Downloads  logo.png  node-v0.4.4  Public    Videos
root@kali:~# md5sum logo.png 
966007c476e0c200fba8b28b250a6379  logo.png
```

__Answer: 966007c476e0c200fba8b28b250a6379__
</div>

## HTTP 2

<a href="/images/ncl14.png"><img src="/images/ncl14.png"></a>

For this challenge we are provided the following file: [NCL-2016-Pre-HTTP 2.pcap](https://jhalon.github.io/download/NCL-2016-Pre-HTTP 2.pcap)

<div class="rBorder" markdown="1">
<span style="color:red">1. __What was the compromised website that was used to infect users with malware?__</span>

Looking though the streams we come across __Referer__ in stream 4. This shows us that someone is requesting another webpage, looking at the __Referer__ URL will provide us the compromised website name.

<a href="/images/ncl-http2-1.png"><img src="/images/ncl-http2-1.png"></a>

__Answer: php.net__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What version of the php was the website using?__</span>

Let's go back to the first stream to see the HTTP Request for __php.net__, and that will provide us the info we need.

<a href="/images/ncl-http2-2.png"><img src="/images/ncl-http2-2.png"></a>

__Answer: 5.4.16__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What version of Apache was the website using?__</span>

Same as above, just look for __PHP__.

<a href="/images/ncl-http2-2.png"><img src="/images/ncl-http2-2.png"></a>

__Answer: 2.2.21__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __In what year was the capture made?__</span>

We can use the current TCP stream and just look for __Date__.

<a href="/images/ncl-http2-2.png"><img src="/images/ncl-http2-2.png"></a>

__Answer: 2013__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __What domain servers up the malicious file?__</span>

We can see that in stream 7 there is a GET request for a __.SWF__ file which is a Shockwave File, and possibly is malicious. (Question 7 basically gives it away...)

<a href="/images/ncl-http2-3.png"><img src="/images/ncl-http2-3.png"></a>

__Answer: zivvgmyrwy.3razbave.info__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __What is the IP address of the malicious domain?__</span>

Just exit out of the TCP stream, and the first packet there should provide us the source IP.

<a href="/images/ncl-http2-4.png"><img src="/images/ncl-http2-4.png"></a>

__Answer: 192.168.40.10__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">7. __At what packet number is the first request for a malicious .SWF made?__</span>

Just as above, the packet where we got the IP also will be the packet # for the .SWF request.

<a href="/images/ncl-http2-4.png"><img src="/images/ncl-http2-4.png"></a>

__Answer: 173__
</div>
<div class="rBorder" markdown="1">
<span style="color:red">8. __What packet number requests the first successfully delivered payload?__</span>

Working in IT Security, I know when a payload is successfully ran since you see __This program cannot be run in DOS mode.__ in the packet captures... so if we go through the streams, we will see packet 213 is the first one to initiate the payload.

<a href="/images/ncl-http2-5.png"><img src="/images/ncl-http2-5.png"></a>

__Answer: 213__
</div>

Alright, that's enough for Part 1 - you can read Part 2 [here]()!

Thanks for reading - and as always, stay tuned for more!
