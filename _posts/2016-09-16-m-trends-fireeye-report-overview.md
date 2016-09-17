---
layout: single
title: "M-Trends 2016: Cyber Threat Report Overview"
header:
  overlay_image: ZenBG.png
  caption: "Mandiant"
related: true
comments: true
---

Another one... over a million records were released to the public; usernames, passwords, credit card information. It's just another breach in a long line of breaches. The year of 2015, and 2016 was pretty big for breaches, affecting major companies and many users worldwide. It's become of norm now, with the ever expanding field of technology... cyber security is gruelingly trying to keep up with the ever evolving threat of cyber crime.

In February, 2016 - Mandiant (now acquired by FireEye) released its prominent 2016 M-Trend Report. This report, provided trends, along with statistics and case studies to show how advanced threats (malicious actors) have evolved over the years; relevantly from 2014-2015. After thoroughly reading this report, and compiling a wide range of data from other source such as [Kaspersky Labs]( http://usa.kaspersky.com/), and [Praesidio]( https://www.defensestorm.com/); I decided to provide a brief overview of the current Cyber Threat Trends Report, it’s data, and list possible mitigation techniques useful for defending companies, and home users alike.


## Overview:
The M-Trends Report begins by explaning to us that there has been an increased activity coming straight from Russia (through single and state sponsed threats), all of them mostly being financially motivated. At the same time Chinese based threats have seemed to balance out with Non-Chinese threats, and malcious actors. Cocurrntly with the increased activity, we have also seen a skyrocket of attacks.

Mandiant reported that with the increase of the activity, there have also been an increase in the amount of company breaches. One would think that a breach in a company would be spotted rather quickly, but the data is quite shocking. It is reported, that the "median" number of days a company is compromised - before the breach was discovered by Mandiant - is a whopping 146 days! This might seem a lot at first, but in all honesty it has improved over the years.

<figure class="align-center">
<a href="/images/m1.png"><img src="/images/m1.png"></a>
</figure> 

Even though, the numbers still seem big, we can say that a 59 day improvement since 2014 is a good thing! With the increase of the cyber security sector, and security awareness, we are slowly getting to a point where breaches are becoming more and more detectable. Mandiant also reported that besides the 146 days it takes them to discover that a company has been compromised, it takes approximately 56 days for a company to internally discover a breach, and a shocking 320 days before a 3rd party notifies the company. It is also stated that over 53% of the breaches are reported though external entities, while 47% of the breaches are reported internally.

With the increase of breaches, there was also an increase in the way attacks were carried out on companies. Ranging from a huge increase in "disruptive attacks", to exporting of PII, and the exploitation of network devices. These three categories of attacks contained the following threat vectors, followed by their subcategories:

* Disruptive Attacks
  * Ransomware and Extortion
  * Deleting & Damaging of Data/Systems
  * Modification of Repositories and Critical Business Data
* PII Leaks
  * Phishing Emails
* Attack on Network Devices

## Disruptive Attacks

Though all cyber-attacks on a company are disruptive to some extent, many specific ones listed in the M-Trends report related to attacks that tried to bring attention to the attacker, attacks that resulted in the release of information to the public - resulting in reputation loss and even consequential embarrassment, and the damaging of critical business functions. These disruptive attacks can bring major consequences to the company affected – from financial loss to the loss of intellectual property. 

Praesidio - in their 2016 infographic - estimated that the average time to resolve a cyber-attack was 46 days, with an average cost to participating organizations of $1,988,544 during the 46-day period. This was representative of a 22% increase from last years estimated average of $1,593,627, which was based upon a 45-day resolution period.

### Ransomware and Extortion

With the first prominence of Ransomware in May of 2005, ransomware has grown to be one of the biggest threats in today’s digital world. Paired together with the increasing threats of blackmail and extortion, companies are having a hard time keeping their data safe, as well as differentiating from real and fake threats that might try to extort the company for money in exchange for stolen documents.

The Russian software company Kaspersky, in their [2014-2016 KSN Ransomware Report](https://securelist.com/analysis/publications/75145/pc-ransomware-in-2014-2016/), stated that between the years of 2014-2015 and 2015-2016, there was an 85% increase in the amount of Ransomware seen. As well as a 5.5 times increase in the amount of crypto ransomware used, along with a 4 times increase in the rise of Mobile Ransomware.

<a href="/images/m2.png"><img src="/images/m2.png"></a>

<a href="/images/m3.png"><img src="/images/m3.png"></a>

<a href="/images/m4.png"><img src="/images/m4.png"></a>

With that rise in Ransomware, there was also a 6.3% rise in the amount of corporate useres affected by Ransomware

<a href="/images/m4.png"><img src="/images/ksn3.png"></a>

Even though Ransomware is done through the use of Malware or Malicious Software, Extortion kind of falls in line with "Ransom". In many cases, unpaid ransoms usually leads to the public release of confidential documents - it's simply done to embarrass the company and bring either financial losses, or reputation damage. Extortion can come in many forms; from emails to c-level executives threatening the use of a DDoS attack on the company, to the release of "possible" stolen documents and intellectual property. 

Much of the ransomware nowadays is requiered to be paid in deregulated currency such as [Bitcoins](https://bitcoin.org/en/), a crypto currency that is hard to track. And based on Mandiat's report, the cost of the Ransomware is usually around the same value as the data they stole (giving us insight that many of these malicious attackers have a good idea of what they are dealing with).

One of these recent extortion breaches can be linked to [Goldcorp's Extortion Bid](http://www.bloomberg.com/news/articles/2016-04-28/goldcorp-confirms-data-breach-and-starts-investigation). The hackers from that breach leaked data that included employee login IDs and passwords, salary and budget documents, and other sensitive corporate and personal information about Goldcorp and its employees.

Based on Praesidio's infographic, it's estimated that around 10,000 records are stolen per incident, and can lead to the total average cost of $6.53 million in loses, an 11% increase from last year. These losses can be from abnormal turnover of customers, increased customer acquisition activities, reputation losses, and diminished goodwill. The average losses in a breach can include:

* $5 - $50 per notification of clients, customers, and other businesses.
* $259 average per comprised record.
* $500,000 average cost of legal proceedings.
* $5,000 - $100,000 in Federal Fines.
* $10 - $30 per person for credit monitoring if PII breach.
* $200 - $2,000 per hour for the cost of a third party forensic examination.

The only downside to extortion based attacks is that it's hard to pinpoint if the source is credible or not, and even if they are, and the ransomware is paid... what are the chances that the attackers will release the data anyways? Even if data is released, it can be taken down fairly quickly, that's why many attackers resort to pastebin and P2P sites like Tor or Torrents to spread the leak.

### Deleting & Damaging of Data/Systems


