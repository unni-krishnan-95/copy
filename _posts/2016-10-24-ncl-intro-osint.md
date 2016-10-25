---
layout: single
title: "NCL CTF - Preseason: Intro & OSINT"
header:
  teaser: oth.png
  overlay_image: nebula.jpg
  caption: "[__NCL__](http://www.nationalcyberleague.org/)"
related: true
comments: true
---

The [National Cyber League](http://www.nationalcyberleague.org/) Fall 2016 Season has officially started! And I am way beyond excited to be competing this year, and to be testing my knowledge against thousands of college students across the nation.

For those that do not know what the National Cyber League is (or NCL for short), let me give you a brief breakdown before I jump into more details and the Preseason Write-ups.

## About the NCL:

The NCL was founded in May 2011 to provide an ongoing virtual training ground for collegiate students to develop, practice, and validate their cybersecurity skills using next-generation high-fidelity simulation environments.

One of the distinguishing factors of the NCL is the integration of learning objectives in all its activities. One of the main ways this is accomplished is by aligning customized content available in NCL Gymnasiums with simulations and games. This allows players to use the Gym environment to develop knowledge and skills and then demonstrate these newly acquired skills in competitive individual and team play. It also allows the NCL to measure player’s game performance and produce individualized reports (NCL Scouting Report) on strengths and weakness amongst various learning objectives and industry-recognized competencies.

The NCL challenges students in the following cyber disciplines:

* Open Source Intelligence
* Scanning
* Enumeration
* Penetration Testing
* Traffic Analysis
* Log Analysis
* Wireless Security
* Cryptography
* Web Application Security

## Fall Season:

The 2016 Fall Season is broken down into 2 portions; the Preseason, and the Regular Season.

### Preseason:

The Preseason Game challenges are based on CompTIA Security+ and EC-Council Certified Ethical Hacker (CEH) performance-based exam objectives and preparatory lab exercise content.
 
Skills being measured in the Preseason Game include:

* Open Source Intelligence
* Network Traffic Analysis
* Log Analysis
* Cryptography
 
Based on the results of this game, players will be placed in one of three brackets (Gold, Silver, and Bronze) in their conference, to facilitate season play amongst individual players with similar knowledge and skill levels.

### Regular Season:

The regular season on the other hand is broken down into 2, 8 hour games - CTF Style. Top players are shown on the scoreboard available publicly on the site.

You can read more about the NCL [here](http://www.nationalcyberleague.org/fall-season)!

## Preseason - Content Overview

Now that we know more about what the NCL is, and what it includes - let's jump into the more technical side of things.

Throughout the Season, and after each Regular Season Game, I will be posting write-ups of how I completed the challenges.

**Please NOTE, that I will be posting everything after the challenge is closed - this is to prevent cheating!**

This years NCL Preseason consisted of the following content.

<a href="/images/ncl1.png"><img src="/images/ncl1.png"></a>

Since we now have a better grasp of what we can expect, let's jump into the first challenge - [OSINT](https://en.wikipedia.org/wiki/Open-source_intelligence)!

## OSINT - Open Source Intelligence

Our first OSINT challenge begins with the following questions.

<a href="/images/ncl2.png"><img src="/images/ncl2.png"></a>

These were all pretty easy to solve, but involved some Google Fu Skills! I'm not going to show where/how to Google the answers - I will just provide the answers with Google Links to where I found them.

<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the CVE of the original POODLE attack?__</span>

You can follow [this](https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2014-3566) link to find the answer.

__Answer: CVE-2014-3566__
</div>


<div class="rBorder" markdown="1">
<span style="color:red">2. __What version of VSFTPD contained the smiley face backdoor?__</span>

You can follow [this](http://www.computersecuritystudent.com/SECURITY_TOOLS/METASPLOITABLE/EXPLOIT/lesson8/) link to find the answer.

__Answer: 2.3.4__
</div>


<div class="rBorder" markdown="1">
<span style="color:red">3. __What was the first 1.0.1 version of OpenSSL that was NOT vulnerable to heartbleed?__</span>

You can follow [this](http://heartbleed.com/) link to find the answer.

__Answer: 1.0.1g__
</div>


<div class="rBorder" markdown="1">
<span style="color:red">4. __What was the original RFC number that described Telnet?__</span>

You can follow [this](https://en.wikipedia.org/wiki/Telnet) link to find the answer.

__Answer: 15__
</div>


<div class="rBorder" markdown="1">
<span style="color:red">5. __How large (in bytes) was the SQL Slammer worm?__</span>

You can follow [this](https://en.wikipedia.org/wiki/SQL_Slammer) link to find the answer.

__Answer: 376__
</div>

Our second OSINT challenge relies on Email Analysis.

<a href="/images/ncl3.png"><img src="/images/ncl3.png"></a>

We are provided with the following email header to answer the questions.

```
Delivered-To: alpha1@hacknet.cityinthe.cloud
Received: by 177.75.184.96 with SMTP id c1234trf3719itc;
        Wed, 9 Sep 2015 11:29:09 -0700 (PDT)
Return-Path: <gh0st@hacknet.cityinthe.cloud>
Received: from mail.hacknet.cityinthe.cloud (mail.hacknet.cityinthe.cloud. [75.184.96.93])
        by mx.cityinthe.cloud with ESMTP id o66si4673783qhb.117.2015.09.09.11.29.08
        for <alpha1@hacknet.cityinthe.cloud>;
        Wed, 09 Sep 2015 11:29:08 -0700 (PDT)
Received: by mail.hacknet.cityinthe.cloud (75.184.96.93) with ESMTP id t89IT8Le023674
	for <alpha1@hacknet.cityinthe.cloud>; Wed, 9 Sep 2015 14:29:08 -0400 (EDT)
From: <gh0st@hacknet.cityinthe.cloud>
Message-Id: <201509091829.t89IT8cb018346@mail.cityinthe.cloud>
Date: Wed, 09 Sep 2015 14:29:08 -0400
To: alpha1@hacknet.cityinthe.cloud
Subject: passphrase
User-Agent: Heirloom mailx 12.4 7/29/08
MIME-Version: 1.0
Content-Type: text/plain; charset=us-ascii
Content-Transfer-Encoding: 7bit

The flood of revolution.
```
<div class="rBorder" markdown="1">
<span style="color:red">1. __What is the recipient’s email address?__</span>

The answer is located in Line 1 of the header - `Delivered-To: alpha1@hacknet.cityinthe.cloud`.

__Answer: alpha1@hacknet.cityinthe.cloud__
</div>


<div class="rBorder" markdown="1">
<span style="color:red">2. __What is the sender’s email address?__</span>

The Return Path in Line 4 provides us this answer - `Return-Path: gh0st@hacknet.cityinthe.cloud`.

__Answer: gh0st@hacknet.cityinthe.cloud__
</div>


<div class="rBorder" markdown="1">
<span style="color:red">3. __What IP address retrieves the email?__</span>

Line 5 provides us this answer - `Received: from mail.hacknet.cityinthe.cloud (mail.hacknet.cityinthe.cloud. [75.184.96.93])`

__Answer: 75.184.96.93__
</div>


<div class="rBorder" markdown="1">
<span style="color:red">4. __What is the content type of the message?__</span>

Line 18 provides us this answer - `Content-Type: text/plain; charset=us-ascii`

__Answer: text/plain__
</div>


<div class="rBorder" markdown="1">
<span style="color:red">5. __What version of MIME is being used?__</span>

Just look for MIME in Line 17 - `MIME-Version: 1.0`.

__Answer: 1.0__
</div>


<div class="rBorder" markdown="1">
<span style="color:red">6. __What day of the week was the message received?__</span>

Look for the date after Recieved in Line 3 - `Wed, 9 Sep 2015 11:29:09 -0700 (PDT)`.

__Answer: Wednesday__
</div>

Alright, that's all for now! Stay tuned for my next NCL post where we will be going over Cryptography.

Thanks for reading!
