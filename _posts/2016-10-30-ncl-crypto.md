---
layout: single
title: "NCL CTF - Preseason: Cryptography"
header:
  teaser: oth.png
  overlay_image: nebula.jpg
  caption: "[__NCL__](http://www.nationalcyberleague.org/)"
related: true
comments: true
---

Today we will be covering the __Cryptography__ portion of the NCL Preseason game. If you don't know what the NCL is, or what these posts are about, then I suggest you go back and read my Introduction Post which can be found [here](https://jhalon.github.io/ncl-intro-osint/)!

Alright, let's begin!

## Crypto 1:

<a href="/images/ncl3.png"><img src="/images/ncl3.png"></a>

<div class="rBorder" markdown="1">
<span style="color:red">1. __0x616761696e74687265653538__</span>

We can tell that this password is in Hex format due to the __0x__ at the start of the password. We can covert the hex to ASCII in Linux by simply running the following command.

```console
root@kali:~# echo 0x616761696e74687265653538 | xxd -r -p
againthree58
```

And there we have it. The output is our password!

__Answer: againthree58__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">2. __cGVvcGxlY3Jvd2Q1MQ==__</span>

This password was Base64 Encoded. We can decode it in our Linux terminal.

```console
root@kali:~# echo cGVvcGxlY3Jvd2Q1MQ== | base64 --decode
peoplecrowd51
```

__Answer: peoplecrowd51__
</div>

<div class="rBorder" markdown="1">
<span style="color:red">3. __01101101 01100001 01110100 01110100 01100101 01110010 01110011 01100001 01101001 01101100 00110110 00110010__</span>

This password was in binary form. You can go [BinaryHexConverter](http://www.binaryhexconverter.com/binary-to-ascii-text-converter) and convert it to ASCII.

__Answer: mattersail62__
</div>

## Crypto 2:

<a href="/images/ncl4.png"><img src="/images/ncl4.png"></a>

<div class="rBorder" markdown="1">
<span style="color:red">1. __znggrefnvy__</span>

Our hint here was "__shift cipher__" so we can assume that this is a [Caesar Cipher](http://practicalcryptography.com/ciphers/caesar-cipher/). Since we do not know the total amount the letters were shifted by, we will have to brute force the cipher.

To do this I went to [Decode.fr](http://www.dcode.fr/caesar-cipher) and used their Brute Force Attack to decrypt all possible passwords.

| Shift         | Password      |
| :-----------: |:-------------:|
|+13		| MATTERSAIL	|
|+24		| BPIITGHPXA	|
|+5		| UIBBMZAIQT	|
|+19		| GUNNYLMUCF	|
|+18		| HVOOZMNVDG	|
|+17		| IWPPANOWEH	|
|+20		| FTMMXKLTBE	|
|+16		| JXQQBOPXFI	|
|+22		| DRKKVIJRZC	|
|+25		| AOHHSFGOWZ	|
|+6		| THAALYZHPS	|
|+23		| CQJJUHIQYB	|
|+15		| KYRRCPQYGJ	|
|+21		| ESLLWJKSAD	|
|+1		| YMFFQDEMUX	|
|+4		| VJCCNABJRU	|
|+12		| NBUUFSTBJM	|
|+7		| SGZZKXYGOR	|
|+2		| XLEEPCDLTW	|
|+3		| WKDDOBCKSV	|
|+8		| RFYYJWXFNQ	|
|+10		| PDWWHUVDLO	|
|+11		| OCVVGTUCKN	|
|+14		| LZSSDQRZHK	|
|+9		| QEXXIVWEMP	|

We see that __mattersail__ is being used again - as it was previously. So we can assume password reuse, and it would be the correct answer!

__Answer: mattersail__
</div>

## Crypto 3:

<a href="/images/ncl5.png"><img src="/images/ncl5.png"></a>

<div class="rBorder" markdown="1">
<span style="color:red">1. __.--. .-. --- ..- -.. .. .-. --- -.__</span>

This one was pretty simple if you know what you are looking at. This password was in Morse code. So I went to the [Morse Code Translator](http://morsecode.scphillips.com/translator.html) and just pasted in the password to get the answer.

__Answer: PROUDIRON__
</div>

## Crypto 4:

<a href="/images/ncl6.png"><img src="/images/ncl6.png"></a>

For this question we are provided with the following encryption algorithm - written in Python..

```python
def encrypt(str):
	ret = ""
	for char in str:
		ret += rot7(rot3(char))
	return ret
```

<div class="rBorder" markdown="1">
<span style="color:red">1. __qbkl dro owksvc ypp dro wksvcobfob__</span>

Since we already have the code, and know how the password is encrypted - all we have to do is reverse engineer it.

The code is basically taking a string, and for each character in the string it rotates the latter +3, then +7 and adds it to ret. Once done, it returns the string. So for us to get the password from the encryption, all we need to do is the opposite. So rotate the characters +7 then +3. The code will look like the following:

```python
def encrypt(str):
	ret = ""
	for char in str:
		ret += rot3(rot7(char))
	return ret
```

Once you tune the code (__str__ being the encrypted password) we get the answer.

__Answer: grab the emails off the mailserver__
</div>

And that's all for Cryptography - pretty easy I must say! 

Thanks for reading! And stay tuned for the continuation on the NCL Preseason write-ups, VulnHub, and more!
