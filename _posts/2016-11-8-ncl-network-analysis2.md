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

<a href="/images/ncl15.png"><img src="/images/ncl15.png"></a>

For this challenge we are provided the following file: [NCL-2016-Pre-Telnet.pcap](https://jhalon.github.io/download/NCL-2016-Pre-Telnet.pcap)

<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the username that was used to successfully log in?__</span>

First thing we need to do when we open up the pcap is to follow the TPC Stream. Once we do that, we are shown the Telnet stream. Keep in mind that Telnet will echo back each key (except for password) so try not to get confused.

To get our answer just look for "__login__".

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: test__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What is the password that was used to successfully log in?__</span>

Since we already know that the password is not echoed back in telnet, just look for "__password__" and we will have our answer.

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: capture__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What command was executed once the user was authenticated?__</span>

Looking at line 6, we can see that "__$__" is displayed - meaning that this is a command line entry, thus the user has authenticated successfully. This would be the first command execution.

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: uname__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">4. __In what year was this capture created?__</span>

Just look at line 8, and look for what "__date__" uname returned.

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: 2011__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __What is the hostname of the machine that was logged in to?__</span>

Knowing how [uname](https://linux.die.net/man/2/uname) prints out the system information will help us decipher which one is the hostname. Uname displays the hostname as the second object.

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: cm4116__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __What CPU architecture does the remote machine use?__</span>

Just as above, uname returns the machines hardware identifier second to last.

<a href="/images/ncl-telnet-1.png"><img src="/images/ncl-telnet-1.png"></a>

__Answer: armv4tl__
</div>

## Pandora’s Box:

<a href="/images/ncl16.png"><img src="/images/ncl16.png"></a>

For this challenge we are provided the following file: [NCL-2016-Pre-Pandora.pcap](https://jhalon.github.io/download/NCL-2016-Pre-Pandora.pcap)

And we are also provided these instructions for how the protocol works.

<a href="/images/ncl17.png"><img src="/images/ncl17.png"></a>

<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the IP address of the server?__</span>

This challenge was very tricky and required some in depth knowledge of how [TCP/IP](https://en.wikipedia.org/wiki/Internet_protocol_suite) functions. Looking at the Custom Protocol instructions we can see that the first communication is between the Client > Server.

The Client initializes the communication by sending the total number of encryption requests that it wishes to make. IF you know TPC/IP then you would understand that the Client will send out a TPC packet with the __PSH__ Flag, as well as the __ACK__ Flag since the server would be acknowledging the receiving data. You can read more about it [here](https://ask.wireshark.org/questions/20423/pshack-wireshark-capture).

So first thing we must do is set a filter in Wireshark to filter out only __PSH__ and __ACK__. To do that we enter "__tcp.flags.push == 1 && tcp.flags.ack == 1__" in the filter. When we have that set, scroll down till we find the first __[PSH, ACK]__ packet. From here, we are able to tell is the Client IP Address is (source) and what the Server IP Address is (destination).

<a href="/images/ncl-pan-1.png"><img src="/images/ncl-pan-1.png"></a>

__Answer: 10.1.0.20__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __What is the IP address of the Client?__</span>

As explained above, the Destination IP will be the IP Address of the Server.

<a href="/images/ncl-pan-1.png"><img src="/images/ncl-pan-1.png"></a>

__Answer: 10.1.0.217__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __What port is the server listening on?__</span>

Looking at the first __[PSH, ACK]__ packet in the Pandora Communication we can see what port the server is listening to by looking at the __Transmission Control Protocol__ line in the packet, and finding the __Dst Port__.

<a href="/images/ncl-pan-1.png"><img src="/images/ncl-pan-1.png"></a>

__Answer: 42455__
</div>

Since we already know that the client first sends the number of encryptions it wants to do in its initialization message - we can see in the instructions that the next thing the client sends is the "__check__" or a "__fixed 2-bytes integer__". So, let's simply follow the packets TPC Stream to see the information it's sending. After you do, change the "__Show data as:__" to __RAW__. The second line will be the 2-bytes "magic" ID.

<div class="rBorder" markdown="1">
<span style="color:red">4. __What is the magic 2-byte ID in decimal?__</span>

<a href="/images/ncl-pan-2.png"><img src="/images/ncl-pan-2.png"></a>

__Answer: 0417__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">5. __How many encrypt requests were made by the client?__</span>

Just like above, the first line in the TCP stream will provide us this data.

<a href="/images/ncl-pan-2.png"><img src="/images/ncl-pan-2.png"></a>

This data though is in hexadecimal, so we can easily convert it to decimal in our CLI.

```console
root@kali:~# echo $((14#00000005))
5
```

__Answer: 5__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">6. __What is the length (in bytes) of the first encrypt request?__</span>

Looking back at the instructions provided to us. We see that during the Encrypt Request, the second thing the Client sends the server is a "__4-byte integer__" that represents the length of the data, followed by the data to be encrypted.

So a 4-byte integer would be 00 00 00 00, looking closely at line 4 (where the client is sending it's data to be encrypted) we see __00000058__, which will be the 4-byte size integer.

<a href="/images/ncl-pan-2.png"><img src="/images/ncl-pan-2.png"></a>

Once again, the data is in hexadecimal format, so we will convert it to decimal format to get the size.

```console
root@kali:~# echo $((16#00000058))
88
```

__Answer: 88__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">7. __What is the length (in bytes) of the second encrypt request?__</span>

Same as above, just look for the second 4-byte integer that will represent the second portion of the request. We will see that the 2nd request's 4-byte integer is __00000048__.

<a href="/images/ncl-pan-2.png"><img src="/images/ncl-pan-2.png"></a>

As before, we convert hexadecimal to decimal to get our answer.

```console
root@kali:~# echo $((16#00000048))
72
```

__Answer: 72__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">8. __How large is an individual encrypt hash in bytes?__</span>

Looking back at the instruction, we see that after the Client sends all its data, the server responds with a single encrypted response, containing hashes for each request. Simply just click on line 12 in the stream (the blue one - as this is server response) and just look what the data length is in the packet. This will be our "fixed" hash length.

<a href="/images/ncl-pan-3.png"><img src="/images/ncl-pan-3.png"></a>

__Answer: 32__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">9. __What was the encrypt response (in the form of 0xFFFF) for the first request?__</span>

Since we know that the hashes are all 32 bytes long, just grab the first hash (which is already 32 bytes) on line 12, and that will be the answer.

<a href="/images/ncl-pan-4.png"><img src="/images/ncl-pan-4.png"></a>

__Answer: b8c97b08e198fa9ff79a3a9c1f0109b18687b7a1a3ff1772c29b4dc86753d711__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">10. __What was the encrypt response (in the form of 0xFFFF) for the second request?__</span>

This is simple... since line 12 gives us a 32 byte long hash, just match up the length of the first hash to the hash on the next line.

<a href="/images/ncl-pan-5.png"><img src="/images/ncl-pan-5.png"></a>

__Answer: 8817153ae81d94b5d6c745e63d1df31d5d02bd3b030b820c3c038654fdca619c__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">11. __What is the hidden flag being sent with the protocol?__</span>

Since the only thing being sent with the protocol is the "data" (in red), let's go ahead and grab that.

<a href="/images/ncl-pan-6.png"><img src="/images/ncl-pan-6.png"></a>

Once we have that copied, we can convert the data from hexadecimal to ASCII (as it's in plaintext). That will provide us with the following:

```
XTkNMLUZKQ0ctMTYzMiBOQ0wtRkpDRy0xNjMyIE5DTC1GSkNHLTE2MzIgTkNMLUZKQ0ctMTYzMiBO
Q0wtRkpDRy0HxNjMyIE5DTC1GSkNHLTE2MzIgTkNMLUZKQ0ctMTYzMiBOQ0wtRkpDRy0xNjMyIE5D
TC1GSkkNHLTE2MzIgTkNMLUZKQ0ctMTYzMiBOQ0wtRkpDRy0xNjMyIE5DTC1GSkNHLTE2MzIgTkNM
LUZKQ0ctMTYzMiBOQ0wtRkpDRy0xNjMyIE5DWTC1GSkNHLTE2MzIgTkNMLUZKQ0ctMTYzMiBOQ0wt
RkpDRy0xNjMyIE5DTC1GSkNHLTE2MzIgTkNMLUZKQ0ctMT"YzMiBOQ0wtRkpDRy0xNjMyIE5DTC1G
SkN
```

This seems like it's encoded as Base64. So let's go ahead and decode it...

```
NCL-FJCG-1632
```

__Answer: NCL-FJCG-1632__
</div>

That's all for the NCL Preseason - thanks for reading everyone!
