---
layout: single
title: "NCL CTF - Preseason: Network Traffic Analysis (Part 2)"
header:
  teaser: oth.png
  overlay_image: nebula.jpg
  caption: "[__NCL__](http://www.nationalcyberleague.org/)"
related: true
comments: true
---

Welcome back to the continuation of the NCL Preseason Posts! Today we will be covering __Part 2__ of the __Network Traffic Analysis__ portion of the NCL Preseason game - this is also the final content that was presented during this CTF. If you don't know what the NCL is, or what these posts are about, then I suggest you go back and read my Introduction Post which can be found [here](https://jhalon.github.io/ncl-intro-osint/)!

Also, if you missed my previous write-ups for the preseason, you can find the Cryptography portion [here](https://jhalon.github.io/ncl-crypto/) and the Log Analysis portion [here](https://jhalon.github.io/ncl-log-analysis/)!

So without any further ado - let's get to it!

## Telnet:

<a href="/images/ncl14.png"><img src="/images/ncl14.png"></a>

For this challenge we are provided the following file: [NCL-2016-Pre-Telnet.pcap](https://jhalon.github.io/download/NCL-2016-Pre-Telnet.pcap)

<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the username that was used to successfully log in?__</span>

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: test__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What is the password that was used to successfully log in?__</span>

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: capture__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What command was executed once the user was authenticated?__</span>

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: uname__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __In what year was this capture created?__</span>

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: 2011__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __What is the hostname of the machine that was logged in to?__</span>

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: cm4116__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __What CPU architecture does the remote machine use?__</span>

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: armv4tl__
</div>

## Pandora’s Box:

<a href="/images/ncl15.png"><img src="/images/ncl15.png"></a>

For this challenge we are provided the following file: [NCL-2016-Pre-Pandora.pcap](https://jhalon.github.io/download/NCL-2016-Pre-Pandora.pcap)

And we are also provided these instructions for how the protocol works.

<a href="/images/ncl16.png"><img src="/images/ncl16.png"></a>

<div class="rBorder" markdown="1">
<span style="color:red">1. What is the IP address of the server?__</span>

<a href="/images/ncl-pan-1.png"><img src="/images/ncl-pan-1.png"></a>

__Answer: 10.1.0.20__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What is the IP address of the Client?__</span>

<a href="/images/ncl-pan-1.png"><img src="/images/ncl-pan-1.png"></a>

__Answer: 10.1.0.217__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What port is the server listening on?__</span>

<a href="/images/ncl-pan-1.png"><img src="/images/ncl-pan-1.png"></a>

__Answer: 60123__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __What is the magic 2-byte ID in decimal?__</span>

<a href="/images/ncl-pan-2.png"><img src="/images/ncl-pan-2.png"></a>

__Answer: 0417__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __How many encrypt requests were made by the client?__</span>

<a href="/images/ncl-pan-2.png"><img src="/images/ncl-pan-2.png"></a>

```console
root@kali:~# echo $((14#00000005))
5
```

__Answer: 5__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __What is the length (in bytes) of the first encrypt request?__</span>

<a href="/images/ncl-pan-2.png"><img src="/images/ncl-pan-2.png"></a>

```console
root@kali:~# echo $((16#00000058))
88
```

__Answer: 78__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">7. __What is the length (in bytes) of the second encrypt request?__</span>

<a href="/images/ncl-pan-2.png"><img src="/images/ncl-pan-2.png"></a>

```console
root@kali:~# echo $((16#00000048))
72
```

__Answer: 64__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">8. __How large is an individual encrypt hash in bytes?__</span>

<a href="/images/ncl-pan-3.png"><img src="/images/ncl-pan-3.png"></a>

__Answer: 32__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">9. __What was the encrypt response (in the form of 0xFFFF) for the first request?__</span>

<a href="/images/ncl-pan-4.png"><img src="/images/ncl-pan-4.png"></a>

__Answer: b8c97b08e198fa9ff79a3a9c1f0109b18687b7a1a3ff1772c29b4dc86753d711__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">10. __What was the encrypt response (in the form of 0xFFFF) for the second request?__</span>

<a href="/images/ncl-pan-5.png"><img src="/images/ncl-pan-5.png"></a>

__Answer: 8817153ae81d94b5d6c745e63d1df31d5d02bd3b030b820c3c038654fdca619c__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">11. __What is the hidden flag being sent with the protocol?__</span>

<a href="/images/ncl-pan-6.png"><img src="/images/ncl-pan-6.png"></a>

```
XTkNMLUZKQ0ctMTYzMiBOQ0wtRkpDRy0xNjMyIE5DTC1GSkNHLTE2MzIgTkNMLUZKQ0ctMTYzMiBO
Q0wtRkpDRy0HxNjMyIE5DTC1GSkNHLTE2MzIgTkNMLUZKQ0ctMTYzMiBOQ0wtRkpDRy0xNjMyIE5D
TC1GSkkNHLTE2MzIgTkNMLUZKQ0ctMTYzMiBOQ0wtRkpDRy0xNjMyIE5DTC1GSkNHLTE2MzIgTkNM
LUZKQ0ctMTYzMiBOQ0wtRkpDRy0xNjMyIE5DWTC1GSkNHLTE2MzIgTkNMLUZKQ0ctMTYzMiBOQ0wt
RkpDRy0xNjMyIE5DTC1GSkNHLTE2MzIgTkNMLUZKQ0ctMT"YzMiBOQ0wtRkpDRy0xNjMyIE5DTC1G
SkN
```

Base64 Decode...

```
NCL-FJCG-1632
```

__Answer: NCL-FJCG-1632__
</div>

That's all for the NCL Preseason - thanks for reading everyone!
