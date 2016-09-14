---
layout: single
title: "OverTheWire: 'Natas' Solutions 1-10"
header:
  teaser: oth.png
  overlay_image: ZenBGG.png
  caption: "[__OverTheWire__](http://overthewire.org/wargames/)"
related: true
comments: true
---

Web Hacking; one of the most dangerous attack vectors out on the internet in today's world. Web Hackers have gotten away with millions of user accounts and passwords, credit card information, and even social security numbers! 

You might wonder how this is even possible?! But we need to understand, that many websites such as Facebook, Google, and even Amazon, store all your information in SQL Databases. These databases are connected to the web servers, allowing them to process user transactions, login requests, and a countless amount of other things! These servers also handle user encryption, session keys, etc. One coding mistake; allowing a malicious attacker to inject SQL code into a query, or even inject special characters into a form, or the URL, can be devastating!

Today, White Hat Hackers (Penetration Testers) must be well versed in many disciplines including web hacking and secure coding. Learning these disciplines allows pen testers to find web vulnerabilities, and coding exploits that could be used to cause a loss of confidentiality. From these assessments, pen testers provide companies information on how to secure their code, and websites to prevent such devastating attacks.

Today, I will be going over __Natas__, which can be found at [OverTheWire]( http://overthewire.org/wargames/natas/). __Natas__ is here to help teach the basics of server side-web-security, ranging from Replay Attacks, Header Manipulation, Directory Traversal, etc.

Each level of Natas consists of its own website located at __http://natasX.natas.labs.overthewire.org__, where X is the level number. Each level has access to the password of the next level. Your job is to somehow obtain that next password and level up. __All passwords are also stored in /etc/natas_webpass/__.

So, let's begin!

### Level 0:
Since we are not using SSH, we will be using a web browser for this. Let's open up a browser and login to Natas0 by going to __http://natas0.natas.labs.overthewire.org__ and using the username: __natas0__ and the password: __natas0__.

<a href="/images/natas0.png"><img src="/images/natas0.png"></a>

Once we are logged in, the level hint will appear in the middle of the screen; such as below.

<a href="/images/natas0-1.png"><img src="/images/natas0-1.png"></a>

This level is pretty simple, just __Right Click__ > __View Page Source__.

```html
<body>
<h1>natas0</h1>
<div id="content">
You can find the password for the next level on this page.

<!--The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto -->
</div>
</body>
```

Looking at the HTML code we can see the `<!-- -->` (comment) section displaying the password. 

Congrats, you passed level 0!

### Level 1:

<a href="/images/natas1.png"><img src="/images/natas1.png"></a>

For this level, sine we can't use __Right Click__, so we will go ahead and press __F12__. This should bring up the developer window; such as below.

<a href="/images/natas1-1.png"><img src="/images/natas1-1.png"></a>

Go to the __console__ section, and you will be able to view the HTML code.

```html
<div id="content">
You can find the password for the next level on this page, but rightclicking has been blocked!

<!--The password for natas2 is ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi -->
</div>
```

### Level 2:

<a href="/images/natas2.png"><img src="/images/natas2.png"></a>

Nothing on the page? Yah, right... doubt it! Let's go ahead and View Page Source.

```html
<body>
<h1>natas2</h1>
<div id="content">
There is nothing on this page
<img src="files/pixel.png">
</div>
</body>
```
It seems, that there is a image file linked in the HTML code. Let's go ahead and add __/files__ to the end of the URL. It should look something like this: __http://natas2.natas.labs.overthewire.org/files/__. Once done you will see a page displayed; such as below.

<a href="/images/natas2-1.png"><img src="/images/natas2-1.png"></a>

__users.txt__ seems promising, let's click that and see what we get.

```
# username:password
alice:BYNdCesZqW
bob:jw2ueICLvT
charlie:G5vCxkVV3m
natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
eve:zo4mJWyNj2
mallory:9urtcpzBmH
```

Alright, we got the password! Moving on to level 3!

### Level 3:

<a href="/images/natas3.png"><img src="/images/natas3.png"></a>

Again? Liars! Let's View Page Source, again...

```html
<body>
<h1>natas3</h1>
<div id="content">
There is nothing on this page
<!-- No more information leaks!! Not even Google will find it this time... -->
</div>
</body>
```
"__Not even Google will find it this time...__" is our hint here. If you have some idea of HTML, and about web servers, then you would know that the files it's referring too is __robots.txt__. If you have no idea what it is, then you can read more about it [here](http://www.robotstxt.org/)!

```
User-agent: *
Disallow: /s3cr3t/
```

Okay, so the __robots.txt__ is disallowing crawlers to find __/s3cr3t/__. Let's go ahead and add it to the end of the webpage, which should look something like this: __http://natas3.natas.labs.overthewire.org/s3cr3t/__.

<a href="/images/natsa3-1.png"><img src="/images/natas3-1.png"></a>

__users.txt__ is the only file we can click... so let's do just that!

```
natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
```

Fairly easy, we got the password and can move on to level 4!

### Level 4:

<a href="/images/natas4.png"><img src="/images/natas4.png"></a>

This level is really interesting, and is the first one to introduce us to [Burp](https://portswigger.net/burp/)! The website is telling us that we are not allowed access to the website, and that the only authorized user should be coming from __http://natas5.natas.labs.overthewire.org/__ -- aka... the user has to be __natas5__. 

In general, this is referring to the "[HTTP Referrer](https://en.wikipedia.org/wiki/HTTP_referer)". So let's go ahead and see if we can spoof it! Let's begin by firing up __Burp__, and making sure our proxy is set up for __localhost__ @ 127.0.0.1. Your set up should look something like the image below. If you are having trouble setting up Burp, please refer to [this video](https://portswigger.net/burp/tutorials/UsingBurpProxy.html).

<a href="/images/natas4-1.png"><img src="/images/natas4-1.png"></a>

Since I'm using __Firefox__, I have to set up my network settings to allow Firefox to use my localhost proxy. To do that in Firefox, __Open the Menu__ > __Preferences__ > __Advanced__ > __Network__ > __Connection Settings...__, and make sure you set it up like the image below.

<a href="/images/natas4-2.png"><img src="/images/natas4-2.png"></a>

Once we got Burp running, let's reload the website and go back to Burp. To see the intercepted packet in Burp, go to __Proxy__ > __Intercept__. You should see the following packet header information.

```html
GET /index.php HTTP/1.1
Host: natas4.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:45.0) Gecko/20100101 Firefox/45.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://natas4.natas.labs.overthewire.org/
Authorization: Basic bmF0YXM0Olo5dGtSa1dtcHQ5UXI3WHJSNWpXUmtnT1U5MDFzd0Va
Connection: close
```

As you can see the packet's __Referrer__ is set to: "__http://natas4.natas.labs.overthewire.org/__". Let's go ahead and change that to "__http://natas5.natas.labs.overthewire.org/__". Once done, click __Forward__, and we should get the password `iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq`!

__Note:__ Once done, go back to Network Settings and select "__Use System Proxy Settings__" so you can have a normal connection, without it routing through Burp.

### Level 5:

<a href="/images/natas5.png"><img src="/images/natas5.png"></a>

Again, we can see we don't have access to the webpage because we are not logged in. Let's fire up Burp Suite and see if we can intercept the packet for the natas5. 

```html
GET /index.php HTTP/1.1
Host: natas5.natas.labs.overthewire.org
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:45.0) Gecko/20100101 Firefox/45.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Cookie: loggedin=0
Authorization: Basic bmF0YXM1OmlYNklPZm1wTjdBWU9RR1B3dG4zZlhwYmFKVkpjSGZx
Connection: close
Cache-Control: max-age=0
```
As we can see, the packet header stores cookie information. Let's change __loggedin=0__ to __loggedin=1__, and Forward that packet.

If successfully done, we should get the password `aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1`.

### Level 6:

<a href="/images/natas6.png"><img src="/images/natas6.png"></a>

Alright, for this level we are to enter a secret, and the query __should__ return the password... hopefully! Let 's go ahead and click __View sourcedode__ and we should get the below PHP script.

```php
<?

include "includes/secret.inc";

    if(array_key_exists("submit", $_POST)) {
        if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
    }
?>
```

It seems that the PHP is including a link to a file stored on the webpage __/includes/secret.inc__. Let's go ahead and add that to the end of our URL, like so: __http://natas6.natas.labs.overthewire.org/includes/secret.inc__. We should come up to a blank webpage, so let's View Page Source.

```php
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```

Another PHP script, with the secret code we need. Let's go back to the home page and enter it. If correct, we should get the password `7z3hEENjQtflzgnT29q7wAvMNfZdh0i9`.


### Level 7:

<a href="/images/natas7.png"><img src="/images/natas7.png"></a>

On this level it seems we are provided with 2 links, __Home__ and __About__. Let's View Page Source, and see if we can find anything.

```html
<div id="content">

<a href="index.php?page=home">Home</a>
<a href="index.php?page=about">About</a>
<br>
<br>
this is the front page

<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->
</div>
```

Alright, the HTML comment is telling us that we can get the password from __etc/natas_webpass/natas8__. Judging by the hint, I assume this is a [Directory Traversal Attack](http://www.acunetix.com/websitesecurity/directory-traversal/). 

If we click on __Home__ our URL should display __http://natas7.natas.labs.overthewire.org/index.php?page=home__. Let's go ahead and remove __home__ and add __/etc/natas_webpass/natas8__. The URL should look like so: __http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8__. 

If done correctly, we should get the password `DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe`.

### Level 8:

<a href="/images/natas8.png"><img src="/images/natas8.png"></a>

Another secret key, let's go ahead and view sourcecode. We should see a PHP script like the one below...

```php
<?

$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}

if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
    print "Access granted. The password for natas9 is <censored>";
    } else {
    print "Wrong secret";
    }
}
?>
```

It seems that the secret code we need is encoded. Looking though the PHP code we can see that the "secret" entered is converted from bin to hex, reversed, and then base64 encoded.

So for us to get the "secret" we have to reverse engineer this. Let's begin by opening the console, and start up PHP with `php -a`. We can get the secret key from the encoded key by base64 decoding it, reversing the string, and converting the hex back to bin.

```console
root@kali:`# php -a
Interactive mode enabled

php > echo base64_decode(strrev(hex2bin('3d3d516343746d4d6d6c315669563362')));
oubWYf2kBq
```

If done correctly, we should get the secret key `oubWYf2kBq`. Let's enter that and see if it works.

Congrats, we got the password `W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl`! Moving on to level 9!

### Level 9:

<a href="/images/natas9.png"><img src="/images/natas9.png"></a>

For this level, it seems that the query is looking for words containing our input. Let's view the sourcecode.

```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
?>
```

From the way "key" is being used in the PHP script, we can probably insert arbitrary code. Let me explain! -- If we type in the word "password" then the __passthru__ command in the PHP script will look like so: `grep -i password dictionary.txt`. Seeing the way that key is encapsulated in quotes, and there is no input filtering, we can assume that we are able to enter special characters.

We can use the `;` command separator, which will allow us to use 2 commands in one line. And we will also use the `#` comment command, which will comment out the rest of the text following the symbol.

So, in the input field we will type `; cat /etc/natas_webpass/natas10 #` which in turn will run the __passthru__ command as such; `grep -i ; cat /etc/natas_webpass/natas10 #`, commenting out and removing __dictionary.txt__. 

Congratulations, we got the password `nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu`! We can now move onto level 10!

### Level 10:

<a href="/images/natas10.png"><img src="/images/natas10.png"></a>

This level is similar to the previous level, so let's view the sourcecode and see what we can find in the PHP script.

```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
}
?>
```

Okay, so the script seems to be the same as level 9's, but now they are filtering the `;` and `&` command.

Seems they still haven't fixed the way "key" is storing input. So we can exploit this the same way we did in 9; but this time just using regular expressions.

Let's go ahead and enter `.* /etc/natas_webpass/natas11 #` inside the query. By entering `.*`, we tell `grep` to search for all, while ignoring case, and match it to __etc/natas_webpass/natas11__. The `#` command, comments out __dictionary.txt__, preventing any errors from occurring.

Congrats! We got the password `U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK`! We can move on to level 11!

___

Alright, that's all for now folks! Stay tuned for more __Natas__, coming soon! Also expect a Web Camera Hacking POC, and some Raspberry PI projects!
