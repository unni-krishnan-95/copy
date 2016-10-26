---
layout: single
title: "NCL CTF - Preseason: Log Analysis"
header:
  teaser: oth.png
  overlay_image: nebula.jpg
  caption: "[__NCL__](http://www.nationalcyberleague.org/)"
related: true
comments: true
---

Welcome back to the continuation of my NCL Preseason Posts! Today we will be covering the __Log Analysis__ portion of the NCL Preseason game. If you don't know what the NCL is, or what these posts are about, then I suggest you go back and read my Introduction Post which can be found [here](https://jhalon.github.io/ncl-intro-osint/)!

Also, if you missed my previous Cryptography write-up for the preseason, you can find that [here](https://jhalon.github.io/ncl-crypto/).

Just a fair warning that this post will be fairly long - so let's strap in, and get to it!

## History:

<a href="/images/ncl8.png"><img src="/images/ncl8.png"></a>

For this challenge we are provided the following file: {{ site.url }}/download/NCL-2016-Pre-Firefox.sqlite

You must download the file and open it up in a SQL database to solve the challenge. I used the [SQLite Viewer](http://inloop.github.io/sqlite-viewer/) online to access this information.

Once you have the SQL Database uploaded you will be presented with a page like so.

<a href="/images/sql1.png"><img src="/images/sql1.png"></a>

Once you are there, we need to navigate to the users browser history. So we will select __moz_palces__ from the dropdown.

<a href="/images/sql2.png"><img src="/images/sql2.png"></a>

You will be presented with the screen below... When you arrive at that screen, we will now be able to look for the answers to our questions.

<a href="/images/sql3.png"><img src="/images/sql3.png"></a>

<div class="rBorder" markdown="1">
<span style="color:red">1. __What did the user search for on craigslist?__</span>

Looking for "__craiglist__" in the __url__ column, we see that line 244 will provide us with the answer.

<a href="/images/sql4.png"><img src="/images/sql4.png"></a>

__Answer: __
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What was the current price of bitcoin when the user was browsing?__</span>

All we have to look for here is a price in dollars. Line 246 will provide us that answer.

<a href="/images/sql10.png"><img src="/images/sql10.png"></a>

__Answer: 239.5__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What Bitcoin exchange did the user log in to?__</span>

The keyword here is "exchange" so we are looking for a site you can buy and sell Bitcoin, which will be in line 250.

<a href="/images/sql5.png"><img src="/images/sql5.png"></a>

__Answer: coinbase__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __What is the email that was used to log into the exchange?__</span>

Since we don't see any login data - let's look for known emails. Line 268 shows us that he is logging into a gmail account. We can assume that he is using this to verify his bitcoin exchange.

<a href="/images/sql6.png"><img src="/images/sql6.png"></a>

__Answer: b1gbird@gmail.com__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __What was the ID of the Bitcoin transaction that the user looked at?__</span>

Keyword here is "transaction" so let's just look for that in the title - and line 292 should provide us with the answer.

<a href="/images/sql7.png"><img src="/images/sql7.png"></a>

__Answer: 5274cfba585a4b5681527a37f95c76340428916bb7480cef6c545f0a28dcd2d7__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __What was the total value of all the inputs of the Bitcoin transaction?__</span>

For this one, we have to grab and navigate to the [URL](https://blockchain.info/tx/5274cfba585a4b5681527a37f95c76340428916bb7480cef6c545f0a28dcd2d7) from our previous answer in line 292.

Our answer will be in the __Inputs and Outputs__ section of the website.

<a href="/images/sql8.png"><img src="/images/sql8.png"></a>

__Answer: 0.22616302__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">7. __To which IP address did the majority of the Bitcoins in the transaction go?__</span>

For this one - back at the website - just click __Visualize__ and you will be redirected to a map like page. Click the first transaction up top and you will get the IP Address.

<a href="/images/sql9.png"><img src="/images/sql9.png"></a>

__Answer: 176.223.201.198__
</div>

## Nginx:

<a href="/images/ncl9.png"><img src="/images/ncl9.png"></a>

For this challenge we are provided the following file: {{ site.url }}/download/NCL-2016-Pre-access.log

All of my work done with this log involved the use of the Linux [CLI](https://en.wikipedia.org/wiki/Command-line_interface).

<div class="rBorder" markdown="1">
<span style="color:red">1. __How many different IP addresses reached the server?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | cut -d' ' -f 1 | sort | uniq -c | wc -l
47
```

__Answer: 47__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __How many requests yielded a 200 HTTP status?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | grep '" 200' | wc -l
19
```

__Answer: 19__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __How many requests yielded a 400 HTTP status?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | grep '" 400' | wc -l
38
```

__Answer: 38__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __What IP address rang at the doorbell?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | grep "bell" | cut -d' ' -f 1
186.64.69.141
```

__Answer: 186.64.69.141__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __What version of the Googlebot visited the website?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | grep "Googlebot"
66.249.67.130 - - [01/Oct/2015:03:08:10 -0400] "GET /robots.txt HTTP/1.1" 502 166 "-" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
---snip---
```

__Answer: 2.1__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __Which IP address attempted to exploit the shellshock vulnerability?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | grep "/bin/bash" | cut -d' ' -f 1
61.161.130.241
```

__Answer: 61.161.130.241__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">7. __What was the most popular version of Firefox used for browsing the website?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | grep "Firefox" | cut -d' ' -f 18 | sort | uniq -c 
      4 en-US;
      9 Firefox/31.0"
      1 Gecko/20100101
      2 rv:30.N)
```

__Answer: 31__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">8. __What is the most common HTTP method used?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | cut -d' ' -f 6 | sort | uniq -c
      6 ""
     15 "CONNECT
     60 "GET
      1 "HEAD
      1 "POST
      1 "quit"
      4 "\x00"
      1 "\x04\x01\x00P\xC0c\xF660\x00"
      6 "\x04\x01\x00P\xC6\xCE\x0Eu0\x00"
      4 "\x05\x01\x00"
```

__Answer: GET__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">9. __What is the second most common HTTP method used?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | cut -d' ' -f 6 | sort | uniq -c
      6 ""
     15 "CONNECT
     60 "GET
      1 "HEAD
      1 "POST
      1 "quit"
      4 "\x00"
      1 "\x04\x01\x00P\xC0c\xF660\x00"
      6 "\x04\x01\x00P\xC6\xCE\x0Eu0\x00"
      4 "\x05\x01\x00"
```

__Answer: CONNECT__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">10. __How many requests were for \x04\x01\x00P\xC6\xCE\x0Eu0\x00?__</span>

```console
root@kali cat NCL-2016-Pre-access.log | cut -d' ' -f 6 | sort | uniq -c
      6 ""
     15 "CONNECT
     60 "GET
      1 "HEAD
      1 "POST
      1 "quit"
      4 "\x00"
      1 "\x04\x01\x00P\xC0c\xF660\x00"
      6 "\x04\x01\x00P\xC6\xCE\x0Eu0\x00"
      4 "\x05\x01\x00"
```

__Answer: 6__
</div>

## Squid:

<a href="/images/ncl10.png"><img src="/images/ncl10.png"></a>

For this challenge we are provided the following file: {{ site.url }}/download/NCL-2017-Pre-squid_access.log

<div class="rBorder" markdown="1">
<span style="color:red">1. __In what year was this log saved?	__</span>

With this question, let's start by looking at the first line.

```
1286536308.779    180 192.168.0.224 TCP_MISS/200 411 GET http://liveupdate.symantecliveupdate.com/minitri.flg - DIRECT/125.23.216.203 text/plain
```

We can see that the first few numbers represent the time. Since Squid is a Linux Proxy, this time is in Epoch. So all I did was go online to [EpochConverter](http://www.epochconverter.com/) and converted the time. You should get something similar to what I have below.

<a href="/images/squid1.png"><img src="/images/squid1.png"></a>

__Answer: 2010__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __How many milliseconds did the fastest request take?__</span>

Just eyeing the log we can see that at the end, on line 111 we have the fastest request.

__Answer: 5__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __How many milliseconds did the longest request take?__</span>

Just eyeing the log we can see that at the end, on line 113 we have the longest request.

__Answer: 41762__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __How many different IP addresses used this proxy service?__</span>

```console
root@kali:~# cat NCL-2017-Pre-squid_access.log | cut -d'T' -f 1 | egrep -o '([0-9]{1,3}\.){3}[0-9]{1,3}' | sort | uniq | wc -l
4
```

__Answer: 4__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __How many GET requests were made?__</span>

```console
root@kali:~# cat NCL-2017-Pre-squid_access.log | grep "GET" | wc -l
35
```

__Answer: 35__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __How many POST requests were made?__</span>

```console
root@kali:~# cat NCL-2017-Pre-squid_access.log | grep "POST" | wc -l
78
```

__Answer: 78__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">7. __What company created the antivirus used on the host at 192.168.0.224?__</span>

```console
root@kali:~# cat NCL-2017-Pre-squid_access.log | grep "192.168.0.224"
1286536308.779    180 192.168.0.224 TCP_MISS/200 411 GET http://liveupdate.symantecliveupdate.com/minitri.flg - DIRECT/125.23.216.203 text/plain
1286536308.910     37 192.168.0.224 TCP_MISS/200 4083 GET http://liveupdate.symantecliveupdate.com/streaming/norton$202009$20streaming$20virus$20definitions_1.0_symalllanguages_livetri.zip - DIRECT/125.23.216.203 application/zip
```

__Answer: symantec__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">8. __What url is used to download an antivirus update?__</span>

```console
root@kali:~# cat NCL-2017-Pre-squid_access.log | grep "192.168.0.224" | cut -d' ' -f 11
http://liveupdate.symantecliveupdate.com/streaming/norton$202009$20streaming$20virus$20definitions_1.0_symalllanguages_livetri.zip
```

__Answer: http://liveupdate.symantecliveupdate.com/streaming/norton$202009$20streaming$20virus$20definitions_1.0_symalllanguages_livetri.zip__
</div>

That's all for now, thanks for reading - and stay tuned for more!
