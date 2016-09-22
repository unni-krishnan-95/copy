---
layout: single
title: "OverTheWire: 'Natas' Solutions 11-20"
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

If you know what a [XOR Cipher](https://en.wikipedia.org/wiki/XOR_cipher) is then you would remeber that _A_ __XOR__ _B_ = _C_.

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

With this new cookie, let's go back to Burp and submit it to the page. If done correctly, we should get the password `EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3`. Now we can move on to natas12!

### Level 12:


