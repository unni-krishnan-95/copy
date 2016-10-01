---
layout: single
title: "M-Trends 2016: Cyber Threat Report Overview"
header:
  overlay_image: ZenBG.png
  caption: "Mandiant"
related: true
comments: true
---

Another one... over a million records were released to the public; usernames, passwords, credit card information. It's just another breach in a long line of breaches. The year of 2015, and 2016 was pretty big for cyber attacks, affecting major companies and many users worldwide. It's become of norm now, with the ever expanding field of technology... cyber security is gruelingly trying to keep up with the ever evolving threat of cyber crime.

In February, 2016 - [Mandiant](https://www.fireeye.com/services.html) (now acquired by FireEye) released its prominent M-Trend Report. This report, provided trends, along with statistics and case studies to show how advanced threats (malicious actors) have evolved over the years; relevantly from 2014-2015. After thoroughly reading this report, and compiling a wide range of data from other source such as [Kaspersky Labs]( http://usa.kaspersky.com/), and [Praesidio]( https://www.defensestorm.com/); I decided to provide a brief overview of the current Cyber Threat Trends Report, it’s data, and list possible mitigation techniques useful for defending companies, and home users alike.


## Overview:
The M-Trends Report begins by explaning to us that there has been an increased activity coming straight from Russia (through single and state sponsed threats), all of them mostly being financially motivated. At the same time Chinese based threats have seemed to balance out with Non-Chinese threats, and malicious actors. Cocurrntly with the increased activity, we have also seen a skyrocket of attacks.

Mandiant reported that with the increase of the activity, there have also been an increase in the amount of company breaches. One would think that a breach in a company would be spotted rather quickly, but the data is quite shocking. It is reported, that the "median" number of days a company is compromised - before the breach was discovered by Mandiant - is a whopping 146 days! This might seem a lot at first, but in all honesty it has improved over the years.

<p align="center">
<a href="/images/m1.png"><img src="/images/m1.png"></a>
</p> 

Even though, the numbers still seem big, we can say that a 59 day improvement since 2014 is a good thing! With the increase of the cyber security sector, and security awareness, we are slowly getting to a point where breaches are becoming more and more detectable. Mandiant also reported that besides the 146 days it takes them to discover that a company has been compromised, it takes approximately 56 days for a company to internally discover a breach, and a shocking 320 days before a 3rd party discovers the breach. It is also stated that over 53% of the breaches are reported by external entities, while 47% of the breaches are reported internally.

With the increase of breaches, there was also an increase in the way attacks were carried out on companies. Ranging from a huge increase in "disruptive attacks", to exporting of PII, and the exploitation of network devices. These three categories of attacks contained the following threat vectors:

* Disruptive Attacks
  * Ransomware and Extortion
  * Deleting & Damaging of Data/Systems
  * Modification of Repositories and Critical Business Data
* PII Leaks
  * Phishing Emails
* Attacks on Network Devices

## Disruptive Attacks:

Though all cyber-attacks on a company are disruptive to some extent, many specific ones listed in the M-Trends report, related to attacks that tried to bring attention to the attacker, and attacks that released confidential information to the public - resulting in reputation loss, consequential embarrassment, and the damaging of critical business functions. Such disruptive attacks can bring major consequences to an affected company – from financial loss to the loss of intellectual property. 

Praesidio - in their 2016 [infographic](http://betanews.com/wp-content/uploads/2016/02/Economic_Cost_of_Getting_Hacked.jpg) - estimated that the average time to resolve a cyber-attack was 46 days, with an average cost to participating organizations of $1,988,544 during the 46-day period. This was representative of a 22% increase from last years estimated average of $1,593,627, which was based upon a 45-day resolution period.

### Ransomware and Extortion:

With the first prominence of Ransomware in May of 2005, ransomware has grown to be one of the biggest threats in today’s digital world. Paired together with the increasing threats of blackmail and extortion, companies are having a hard time keeping their data safe, as well as differentiating from real and fake threats that might try to extort the company for money in exchange for stolen documents.

The Russian software company Kaspersky, in their [2014-2016 KSN Ransomware Report](https://securelist.com/analysis/publications/75145/pc-ransomware-in-2014-2016/), stated that between the years of 2014-2015 and 2015-2016, there was an 1.2 increase in the amount of Ransomware seen. As well as a 5.5 times increase in the amount of crypto ransomware used, along with a 4 times increase in the rise of Mobile Ransomware.

<p align="center">
<a href="/images/m2.png"><img src="/images/m2.png"></a>
</p>
<p align="center">
<a href="/images/m3.png"><img src="/images/m3.png"></a>
</p>
<p align="center">
<a href="/images/m4.png"><img src="/images/m4.png"></a>
</p>
With that rise in Ransomware, there was also a 6.3% rise in the amount of corporate useres affected by Ransomware
<p align="center">
<a href="/images/ksn3.png"><img src="/images/ksn3.png"></a>
</p>
Even though Ransomware is done through the use of Malware or Malicious Software, Extortion kind of falls in line with "Ransom". In many cases, unpaid ransoms usually leads to the public release of confidential documents - it's simply done to embarrass the company and bring either financial losses, or reputation damage. Extortion can come in many forms; from emails to c-level executives, and emails threatening the use of a DDoS attack on the company, to the release of "possible" stolen documents and intellectual property. 

Much of the ransomware nowadays is requiered to be paid in deregulated currency such as [Bitcoins](https://bitcoin.org/en/), a crypto currency that is hard to track. And based on Mandiat's report, the cost of the Ransomware is usually around the same value as the data the attackers stole or encrypted; giving us insight that many of these malicious attackers have a good idea of what they are dealing with.

One of these recent extortion breaches can be linked to [Goldcorp's Extortion Bid](http://www.bloomberg.com/news/articles/2016-04-28/goldcorp-confirms-data-breach-and-starts-investigation). The hackers from that breach leaked data that included employee login IDs and passwords, salary and budget documents, and other sensitive corporate and personal information about Goldcorp and its employees.

Based on Praesidio's [infographic](http://betanews.com/wp-content/uploads/2016/02/Economic_Cost_of_Getting_Hacked.jpg), it's estimated that around 10,000 records are stolen per incident, and can lead to the total average cost of $3.72 million in loses. These losses can be from abnormal turnover of customers, increased customer acquisition activities, reputation losses, and diminished goodwill. The average losses in a breach can include:

* $5 - $50 per notification of clients, customers, and other businesses.
* $259 average per comprised record.
* $500,000 average cost of legal proceedings.
* $5,000 - $100,000 in Federal Fines.
* $10 - $30 per person for credit monitoring if PII breach.
* $200 - $2,000 per hour for the cost of a third party forensic examination.

The only downside to extortion based attacks is that it's hard to pinpoint if the source is credible or not, and even if they are, and the ransomware is paid... what are the chances that the attackers will release the data anyways? Even if data is released, it can be taken down fairly quickly, that's why many attackers resort to using pastebin and P2P sites like Tor or Torrents to spread the leak. Making it much harder to contain the leak and prevent the spread of propriety information.

### Deleting & Damaging of Data/Systems:

The deletion and damaging of systems speaks for itself, the after effects of such an attack can be devastating to a company - putting production at a standstill, causing major outages worldwide for users, and incurring massive financial losses. In the M-Trend's report it is stated that in a lot of breaches, threat actors had access to system-level accounts which were capable of deleting and damaging data/system... but instead they decided to covertly steal credit card data, PII, and intellectual property; going to show that many malicious actors are financially motivated and really don’t care on disrupting the company’s operations. 

Mandiant in the M-Trend's report also stated, and I quote:

> "*We’ve investigated multiple incidents where attackers wiped critical business systems and, in some cases, forced companies to rely on paper and telephone-based processes for days or weeks as they recovered their systems and data. We have even seen attackers wipe system backup infrastructure in an effort to keep victims offline longer.*" 

Proving, that many of these companies either didn't have proper backups, or business continuity plans put in place, for such incidents.

### Modification of Repositories and Critical Business Data:

Though not heard of, malicious actors at times will attempt to modify company repositories and critical business data to impact certain aspects of the company and its operations. For example, if a company was in charge of creating iOS and Android applications, a malicious actor can edit the code repositories for the applications and implement a back door for personal gain. Now, business critical data is any kind of information or data that a business would not be able to recover if it was lost. This could include things such as:

* Customer information
* Financial records
* Emails
* Sales records
* Human resource information
* Inventory
* Specification documents
* Vendor/Supplier contacts and information

So if during a breach this information was modified, deleted, or tampered with any way, it can cause lots of confusion and damages to the company, partners, suppliers, and more!

## PII Leaks

PII or Personally Identifiable Information, is information that can be used on its own or with other information to identify, contact, or locate a single person, or to identify an individual in context. Much of this PII data can be used to gain private information such as Social Security, credit cards, etc. At times during breaches PII is also stolen as a byproduct of copying over files, and isn't of particular interest to an attacker, but other times - it's very highly sought. Mandiant so far has no idea how malicious attackers are leveraging the PII data, they do believe that they are using it for the following:

* Bypassing Identify Verification and Access Management Schemes
* Facilitating “Traditional” Espionage Operations & Identifying and Recruiting Insider Threats and Subject Matter Experts
* Targeting Specific Populations for Identification and Monitoring

### Phishing Emails:

Phishing emails are not the thing of the past, year after year they come up with new spam campaigns to try and infect users with anything from backdoors to crypto ransomware. All the user has to do is click on a link or an attachment, and the malicious actor can gain access to the users system. From there, reconnaissance can take place to footprint servers and other computer in search of passwords, domain accounts, PII, and anything else the attacker might favorite. 

Phishing can come in many forms - [spear phishing](http://us.norton.com/spear-phishing-scam-not-sport/article) campaigns are carried out against certain users with relatable information including names, dates, and personal facts. While [whaling](http://www.infoworld.com/article/2621583/phishing/how-to-stop-your-executives-from-being-harpooned.html) attacks are carried out against c-level executives, and if successful can bode lots of success for an attacker. Phishing can also be carried out through the phone in the form of a vishing attack, where the malicious actor might try to harvest usernames, passwords, and anything else they might like, all through social engineering.

There were many famous breaches from 2014-2016 that used social engineering and phishing to steal employee W-2 Forms, and Tax Information, along with their PII such as name, date of birth, address, and social security. You can read more about these types of breaches [here](http://www.csoonline.com/article/3048263/security/phishing-attacks-targeting-w-2-data-hit-41-organizations-in-q1-2016.html)!

## Attacks on Networking Devices:

Reading about attackers compromising networking equipment such as switches, routers, and firewalls is kind of shocking. These devices are critical components to a company’s infrastructure and are usually overlooked by incident response teams and forensic experts as being compromised. Mandiant in their report stated that they have observed such compromises of these networking devices, and have identified backdoors and means of remote access to either control, damage, or circumvent security during a breach.

Some of us reading this might be wondering - as to why attackers would want to compromise these networking devices? Well it's pretty simple really, some examples provided by Madiant are:

* Traffic Monitoring
* Reconnaissance
* Subversion of Security Controls
* Persistence
* Disruption

The only problem with these types’ attacks is that we lack the tools that can discover such compromises, and even if we are able to analyze such devices, it's very time consuming and complex to scale properly during a single incident response or forensic examination.

Such attacks on networking devices consisted of:

* Modification of Cisco Router Images
* XSS (Cross Site Scripting) a Cisco ASA VPN Concentrator
  * Use of [CVE-2014-3393](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3393)
* Cisco IOS Router Backdoors
  * [SYNFUL Knocks](https://www.fireeye.com/blog/threat-research/2015/09/synful_knock_-_acis.html)

Overall much of these attacks are outdated, but we have to understand that these attacks were either possible though means of weak company security, or there weren’t proper policies and procedures in place. Some of you might think as to how policies and procedures could help in a situation like this, and I will explain so in the next section of “mitigation strategies” below.

## Mitigation Strategies and Recommendations:

In today's world nothing is 100% secure, and your company will encounter a breach at least once. Even though a breach in inevitable, you can takes steps to protect yourself, your data, and make it much harder for a malicious actor to exploit your company.

Mandiant in their M-Trends report stated that many of the companies they worked with were unable to identify ongoing security threats within their company. For example, during a Red Team test, less than 10% of the companies responded appropriately to a [Mimikatz](https://github.com/gentilkiwi/mimikatz) AV detection. For those that don't know what mimikatz is, it's a tool that can extract plaintext passwords, hashes, Kerberos tickets from memory, and also preform pass-the-hash. Malicious actors can also dump the [SAM File](https://en.wikipedia.org/wiki/Security_Account_Manager) that can provide them with user passwords.

Many malicious actors can gain these credentials from hashes, or memory dumps due to weak password policies, and improper hashing + salting. So to protect yourself and increase security, make sure you do the following:

* __Implement Strong Password Polices__: Make sure you are using a minimum of 8 characters, with the use of upper case, lower case, numbers and symbols. Also enable password history to prevent the reuse of old passwords. At the same time prevent the use of dictionary words and words relating to any PII. If you like, you can also have your password policy use a wordlist to make sure that the passwords do not correlate to any leaked passwords from recent breaches.
* __Encryption, Hashing, and Salting__: Make sure any data files that include propriety information, company secrets, PII, or critical data is encrypted with a strong encryption passphrase. This includes: file encryption, database filed encryption, and hard disk encryption, as well as SSL/TLS encryption for information being transported across the net. PGP/GPG can also be used with signatures in emails to provide integrity and confidentiality. Hashing passwords along with salting them in AD will prevent malicious actors from cracking cached passwords from SAM files, Kerberos ticket, etc. I suggest you use SHA Hashing instead of MD5 due to its susceptibility of being cracked.

As for your infrastructure devices, security infrastructure, and tools such as SIEM’s, vaults, HIPS, Firewall, ACLs: 

* __Use Strong Authentication__: Using multifactor authentication such as a password and hardware tokens will increase authentication security, and make it much hard for malicious actors to authenticate to corporate devices. Such authentication techniques using passwords and pins will not work since they can be guessed or brute forced. We must use each authentication factor just once, and those factors are - something you know, something you have, something you are, somewhere you are, and something you do.
* __Image Integrity__: If you are storing images for Cisco Devices (or any device for that matter) make sure you use hashes for integrity purposes. A hash of the image can be compared against stored hashes to make sure that the image wasn't tampered with. You can periodically check hashes of running devices, this provides a sense of security and can be the first sign of a breach or untheorized change.
* __Change Management & Patch Management__: Ensure that network administrators keep detailed logs of changes done to networks or the infrastructure. At the same time, include patch management that will ensure all devices are running the current firmware version or current patches. This will help prevent known vulnerabilities and exploits, at the same time it will make it harder for hackers to use known attack vectors.
* __Recovery & Backups__: Make sure you have a recovery and backup plan set up to constantly backup data and images. Also make sure that these backups are stored off-site and in locations that will be inaccessible to any malicious attacker. Your recovery plan should be implemented in with your business continuity planning, to make sure that in case of a breach or data loss, recovery can be put into action - and in a timely manner, restore any data. Note, that this is critical for critical business data such as names, payments, etc.
* __Make sure any OSP is secure and reports any breaches__: Make sure that any OSP (Outsourced Service Provider) you are working with, has good security in place, and reports any security breaches to you right away. This will allow you to monitor for any unusual activity or logins.
* __Monitor Internal Resources, Logins, and Privileged Accounts__: Constantly monitor failed login attempts on critical infrastructure devices, security tools, ACLs, etc. At the same time make sure you monitor any privileged account logins. Privileged Accounts can be used from separate user accounts to follow the “least privilege” principle – this will force admins to use the elevated account to make any critical changes. This helps decrease the attack surface an attacker might have if he cracks an admins account and not his Privileged Account - as it won’t have any permissions to make changes. Also monitoring of privileged accounts instead of user accounts, makes it easier to pinpoint suspicious activity.

With those suggestions there are also a few things to consider about your current security:

* __Are we properly monitoring our perimeter? WAF Implementation, alerting?__: Even though there is monitoring and lots of background noise from port scanners, brute force attacks, exploitation tools, and any other "loud" tools. We must ask, are we properly monitoring against manual attacks - such as sql injection, directory traversal, etc? Are we properly detecting any successful perimeter attacks?
* __How is our Egress Control and Monitoring?__: Are we using all our device capabilities and tools to block malicious or suspicious egress traffic via SSH, RDP, DNS, etc? Are your teams able to detect data theft in progress? Even if DLP, email protection, and network monitoring prevent a connection or certain traffic, can your team be alerted of such occurring incidents?

That's all for this post! Hope you enjoyed reading it as much as I enjoyed writing it. Please provide any feedback, comments, or suggestions in the comments below! Thanks!
