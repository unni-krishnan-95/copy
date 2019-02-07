---
layout: single
title: "Google CTF (2018): Beginners Quest - Introduction"
header:
  overlay_image: google-ctf-banner.jpg
related: true
comments: true
---

Over the past couple of weeks I've been doing a lot of CTFs (Capture the Flag) - old and new. And I honestly can't believe what I've been missing out on. I've learned so much during this time by just playing the CTFs, reading write-ups, and even watching the solutions on YouTube. This allowed me to realize how much I still don't know, and allowed me to see where the gaps in my knowledge were.

One of the CTFs that was particularly interesting to me was the [Google CTF](https://capturetheflag.withgoogle.com/#beginners/). The reason why I really liked Google's CTF was because it allowed for both beginners and experts to take part, and even allowed people new to CTF's to try their hands at some security challenges.

I opted to go for the beginner challenges to see where my skill level really was at - and although it was "mostly" easy, there were still some challenges that had me banging my head on the desk and Googling like a mad man. Even though the Google CTF was over and solutions were online, I avoided them at all costs because I wanted to learn the "hard way".

These beginner challenges were presented in a “Quest” style with a scenario similar to a real world penetration test. Such a scenario is awesome for those who want to sharpen their skills, learn something new about CTFs and security, while also allowing them to see a real world value and impact.

Now, some of you might be wondering... "_How much do I need to know or learn to be able to do a CTF?_" or "_How hard are CTFs?_ 

Truth be told, __it depends__. Some CTFs can be way more complex than other, such as [DEFCON's CTF](https://www.defcon.org/html/links/dc-ctf.html) and even Google's CTF can be quite complex and complicated - but not impossible! It solely depends on your area of expertise.

There are many CTF teams that have people who specialize in Code Review and Web Apps and can do Web Challenges with their eyes closed, but give them a binary and they won't know there difference between the [EIP](https://inst.eecs.berkeley.edu/~cs161/sp15/discussions/dis06-assembly.pdf) and [ESP](https://inst.eecs.berkeley.edu/~cs161/sp15/discussions/dis06-assembly.pdf). The same goes for others! Sure, there are people who are the "Jack of All Trades" and can do pretty much anything, but that doesn't make them an expert in everything. 

After reading this, you might be asking me - _But I've never done a CTF before! How do I know if I'm ready to attempt one?_

Honestly, you'll never be ready! There will always be something new to learn, something new you have never seen before, or something challenging that pushes the limits of your knowledge, even as an expert! That's the whole point of CTFs.

But, there are resources that can help you get started! 

<p align="center"><img src="/images/wtf-ctf.jpg"></p>

Let's start by explaining what a CTF really is!

[CTF Time](https://ctftime.org/ctf-wtf/) does a good job at explaining the basics, so I'm just going to quote them (with some "minor" editing)!

> Capture the Flag (CTF) is a special kind of information security competitions. There are three common types of CTFs: Jeopardy, Attack-Defense and mixed.
> 
> Jeopardy-style CTFs has a couple of questions (tasks) in range of categories. For example, Web, Forensic, Crypto, Binary, PWN or something else. Teams compete against each other and gain points for every solved task. The more points for a task, the more complicated the task. Usually certain tasks appear in chains, and can only be opened after someone on the team solves the previous task. Once the competition is over, the team with the highest amount of points, wins!
> 
> Attack-defense is another interesting type of competition. Here every team has their own network (or only one host) with vulnerable services. Your team has time for patching and usually has time for developing exploits against these services. Once completed, organizers connects participants of the competition to a single network and the wargame starts! Your goal is to protect your own services for defense points and to hack your opponents for attack points. Some of you might know this CTF if you ever competed in the [CCDC](http://www.nationalccdc.org/index.php/component/content/). 
> 
> Mixed competitions may contain many possible formats. They might be a mix of challenges with attack/defense. We usually don't see much of these.
> 
> Such CTF games often touch on many other aspects of security such as cryptography, steganography, binary analysis, reverse engineering, web and mobile security and more. Good teams generally have strong skills and experience in all these issues, or contain players who are well versed in certain areas.

[LiveOverflow](https://www.youtube.com/channel/UClcE-kVhqyiHCcjYwcpfj9w) also has an awesome video explaining CTFs along with examples on each aspect - see below!

{% include video id="8ev9ZX9J45A" provider="youtube" %}

<p align="center"><img src="/images/gs-ctf.jpg"></p>

Now that we have a general idea of what a CTF is and what it contains, let's learn how we can get started in playing CTFs!

Once again, [LiveOverflow](http://liveoverflow.com/intro.html) has an amazing video explaining why CTF's are a great way to learn hacking. This video was a live recording of his FSEC 2017 talk that aimed to "_motivate you to play CTFs and showcase various example challenge solutions, to show you stuff you hopefully haven't seen before and get you inspired to find more interesting vulnerabilities_".

{% include video id="rfjV8XukxO8" provider="youtube" %}

<br>

There are also a ton of resources online that aim to teach you the basics of Vulnerability Discovery, Binary Exploitation, Forensics, and more, such as the following below:

* [CTF Field Guide](https://trailofbits.github.io/ctf/)
* [CTF Resources](https://ctfs.github.io/resources/)
* [Endgame - How To Get Started In CTF](https://www.endgame.com/blog/technical-blog/how-get-started-ctf)
* [CONFidence 2014: On the battlefield with the Dragons -- G. Coldwind, M. Jurczyk](https://www.youtube.com/watch?v=h6oLWmzgDGc)
* [If You Can Open The Terminal, You Can Capture The Flag: CTF For Everyone](https://www.youtube.com/watch?v=b--MeumOcVM)
* [So You Want To Be a Pentester?](https://jhalon.github.io/becoming-a-pentester/) <-- Shameless plug because of resources! =)


Out of all these resources, I believe that [CTF Series: Vulnerable Machines](https://bitvijays.github.io/LFC-VulnerableMachines.html) is honestly the BEST resources for CTFs. It's aim is mostly focused on how to approach Vulnerable VM's like the ones on [VulnHub](https://www.vulnhub.com/) and [Hack The Box](https://www.hackthebox.eu/), but it still gives you a ton of example and resources on how to find certain vulnerabilities, how to utilized given tools, and how to exploit vulnerabilities.

As I said time and time again, learning the basics will drastically help improve your CTF skills. Once you get enough experience you'll start to notice "patterns" in certain code, binaries, web apps, etc. which will allow you to know if a particular vulnerability exists and how it can be exploited.

Another thing that can help you prepare for CTFs is to read write-ups on new bugs and vulnerabilities. A ton of Web CTF challenges are based off of these bugs and vulnerabilities or are a variant of them - so if you can keep up with new findings and understand them, then you're ahead of the curve.

The following links are great places to read about new bugs, and vulnerabilities. They are also a good place to learn how other's exploited known bugs.

{: .notice--info}
__HINT:__ These links can also help you get into Bug Bounty Hunting!

* [Hackerone - Hacktivity](https://hackerone.com/hacktivity)
* [Researcher Resources - Bounty Bug Write-ups](https://forum.bugcrowd.com/t/researcher-resources-bounty-bug-write-ups/1137)
* [Orange Tsai](https://blog.orange.tw/)
* [Detectify Blog](https://blog.detectify.com/)
* [InfoSec Writeups](https://medium.com/bugbountywriteup)
* [Pentester Land - Bug Bounty Writeups](https://pentester.land/list-of-bug-bounty-writeups.html)
* [The Daily Swig - Web Security Digest](https://portswigger.net/daily-swig)

Once we have a decent understanding of a certain field such as Web, Crypto, Binary, etc. it's time we start reading and watching other people's writeups. This will allow us to gain an understanding on how certain challenges are solved, and hopefully it will also teach us a few new things. 

The following links are great places to read and watch CTF solutions:

* [CTF Time - Writeups](https://ctftime.org/writeups)
* [CTFs Github - Writeups, Resources, and more!](https://github.com/ctfs)
* [Mediunm - CTF Writeups](https://medium.com/bugbountywriteup/tagged/ctf)
* [LiverOverflow Youtube](https://www.youtube.com/channel/UClcE-kVhqyiHCcjYwcpfj9w/featured)
* [Gynvael Coldwind](https://www.youtube.com/user/GynvaelEN)
* [Murmus CTF](https://www.youtube.com/channel/UCUB9vOGEUpw7IKJRoR4PK-A/featured)
* [John Hammond](https://www.youtube.com/user/RootOfTheNull)

Now that you have the basics skills and know a little more about certain topics it's time we find a CTF!

[CTF Time](https://ctftime.org/) is still one of the best resources for looking at upcoming events that you can participate in. You can go through the events and see what interests you! Once you choose something, follow the instruction to register and you're done! 

From there, all you need to do is just wait for the CTF to start, and hack away!

Okay, seems easy enough - but then again for a first time it's still overwhelming! So what can we do to make our first CTF experience a good one?

Well, that's where the Google CTF comes in!

<p align="center"><img src="/images/gctf-ctf.jpg"></p>

As I stated before, the reason why I really liked Google's CTF was because it allowed for both beginners and experts to take part, and even allowed people new to CTF's to try their hands at some security challenges without adding too much pressure.

The Beginner Quest starts off with a little back story to "lighten" the mood and let the player know that, this is just a game. We aren't competing for a million dollars, so take it easy and have fun!

The story is as follows:

> Cakes... Throughout history they are long promised, not often delivered. Are they real?
> 
> Are they fabrications of an internal system long designed to tease and tempt you with promises of sweet confectionary goodness that will satisfy and delight? Or the realistic truth of the matter. A dark conspiracy involving many clandestine organizations that want to create content and context around the very existence of this delicacy.
> 
> Your task, uncover the truth, find the cake and show it to the world. Set the truth free.
> 
> You do not have to start this undermining of the Cake-World-Order (cWo) without any information. Our informants deep in the field (some no longer with us), have passed on intel about an operative within the cWo known as Wintermuted. Their home is a mess of old technologies, poor Operational Security (Op-Sec) and Internet of Things (IoT) devices that haven't seen updates in decades, despite being released last year. Start with their rubbish bin! Surely there is a letter or toothpaste tube there with some information that'll get you on the inside.
> 
> Your goal is to get the cake in the fridge... Where else would you put cake in your smart home?

Once we read the story, we can start with the challenges. These beginner challenges were presented in a “Quest” style based off the story scenario. The quest has a total of nineteen (19) challenges as shown below in the quest map - with each color representing a different category as follows:

* <span style="color:purple">Purple:</span> __misc - (Miscellaneous)__
* <span style="color:green">Green:</span> __pwn/pwn-re - (Exploitation/Buffer Overflows & Reverse Engineering)__
* <span style="color:gold">Yellow:</span> __re - (Reverse Engineering)__
* <span style="color:blue">Blue:</span> __web (Web Exploitation)__

<p align="center"><a href="/images/google-ctf-quest-map.png"><img src="/images/google-ctf-quest-map.png"></a></p>

If you click on one of the circles then you will go to the respective challenge. The challenge will contain some information, along with either an attachment or a link. From there, try to solve the challenge and find the flag, which is in the __CTF{}__ format. Submitting the correct flag will complete the challenge.

Now notice how some of these challenges are "grayed out". That's because these challenges are "chained" to one another, meaning that you need to complete the previous one to be able to open the path to the next challenge.

Also notice that Google allows you to make choices on what challenge you want to do. They don't force you to do all of them to get to the __END__, but give you the ability to pick and choose another path if something is too hard. Thus, making it easier for you to feel accomplishment and to later come back and learn!

<p align="center"><img src="/images/gctf-closing.jpg"></p>

Alright, that's it for now. Hopefully you learned something new today and I sincerely hope that the resources will allow you to learn and explore new topics!

The posts following this will detail how I solved the 2018 [Google CTF - Beginners Quest](https://capturetheflag.withgoogle.com/#beginners/), so stay tuned and I hope to see you on the CTF battlefield someday!
