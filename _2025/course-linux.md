---
layout: lecture
title: "#1: Course overview + linux + 🍕"
date: 2025-08-06
ready: true
video:
    aspect: 56.25
    id: Z56Jmr9Z34Q
---

<div class="note">
The video above is part of the original MIT Missing Semester recordings. <br>
While the RUET version of this session will cover the same base material, please expect some differences during the live session.
<br>
<br>
<b> Update 24/07/25: </b> The contents below have been adjusted to reflect the Missing Semester content covered at RUET. Check our <a href="https://github.com/missing-semesters-ruet/missing-semester/commits/master">git history</a> for a full list of changes.

</div>

# Motivation

As computer scientists, we know that computers are great at aiding in repetitive tasks. However, far too often, we forget that this applies just as much to our _use_ of the computer as it does to the computations we want our programs to perform. We have a vast range of tools available at our fingertips that enable us to be more productive and solve more complex problems when working on any computer-related problem. Yet many of us utilize only a small fraction of those tools; we only know enough magical incantations by rote to get by, and blindly copy-paste commands from the internet when we get stuck.

This class is an attempt to address this.

We want to teach you how to make the most of the tools you know, show you new tools to add to your toolbox, and hopefully instill in you some excitement for exploring (and perhaps building) more tools on your own. This is what we believe to be the missing semester from most Computer Science curricula.

# Class structure

The class consists of multiple 1-hour lectures/hack'n'tell sessions running during the first and beginning of second term this year.
For now, we have 14 exciting sessions lined up, introducing you the shell, editors, version control and more.
In essence, we try to cover everything you need to get started as computer scientist frequently working on the command line!

The lectures itself are focused on a
[particular topic]({{'/2024/' | relative_url}}), and most of them are largely independent (with the exception of the different levels of working with the shell). Nonetheless, as the semester goes on we will presume that you are familiar with the content from the earlier lectures. We have lecture notes online, but there will be a lot of content covered in class (e.g. in the form of demos) that may not be in the notes.

The original MIT lectures recorded the lectures and posted the recording online; while our version will be different, they can still provide a good overview of covered topics.

</div>

We are trying to cover a lot of ground over the course, so the lectures may be fairly dense. To allow you some time to
get familiar with the content at your own pace, lectures may include a
set of exercises that guide you through the lecture's key points.
If you have questions after the lecture, feel free to reach out to us on our [Missing Semester Discord Server](https://discord.gg/), or email us at [missingsemesters.ruet@gmail.com](mailto:missingsemesters.ruet@gmail.com).

Due to the limited time we have, we won't be able to cover all the tools
in the same level of detail a full-scale class might. Where possible, we
will try to point you towards resources for digging further into a tool
or topic, but if something particularly strikes your fancy, don't
hesitate to reach out to us and ask for pointers!

Last, we are always trying to extend and optimize our sessions based on your feedback, our interests, and suggestions from the School of Computer Science.
If you would like to see anything covered we don't already plan to cover, or want to provide us our suggestions for improvement, please make sure to fill our [feedback form](https://forms.gle/EqEZwGWX4BsY7TFt8).

# Topic 1: The Shell

<div class="note">
Do you want to follow along but don't have a computer with a Unix shell at hand? You can move over to <a href="https://bellard.org/jslinux/">jslinux</a> to run a Linux shell from your browser!

</div>

## What is the shell?

Computers these days have a variety of interfaces for giving them commands; fanciful graphical user interfaces, voice interfaces, and even AR/VR are everywhere. These are great for 80% of use-cases, but they are often fundamentally restricted in what they allow you to do — you cannot press a button that isn't there or give a voice command that hasn't been programmed. To take full advantage of the tools your computer provides, we have to go old-school and drop down to a textual interface: The Shell.

Nearly all platforms you can get your hand on has a shell in one form or another, and many of them have several shells for you to choose from. While they may vary in the details, at their core they are all roughly the same: they allow you to run programs, give them input, and inspect their output in a semi-structured way.

In this lecture, we will focus on the Bourne Again SHell, or "bash" for short. This is one of the most widely used shells, and its syntax is similar to what you will see in many other shells. To open a shell _prompt_ (where you can type commands), you first need a _terminal_. Your device probably shipped with one installed, or you can install one fairly easily.

## Using the shell

When you launch your terminal, you will see a _prompt_ that often looks a little like this:

```console
missing:~$
```

This is the main textual interface to the shell. It tells you that you are on the machine `missing` and that your "current working directory", or where you currently are, is `~` (short for "home"). The `$` tells you that you are not the root user (more on that later). At this prompt you can type a _command_, which will then be interpreted by the shell. The most basic command is to execute a program:

```console
missing:~$ date
Sun Aug  6 16:55:00 BST 2024
missing:~$
```

Here, we executed the `date` program, which (perhaps unsurprisingly) prints the current date and time. The shell then asks us for another command to execute. We can also execute a command with _arguments_:

```console
missing:~$ echo hello
hello
```

In this case, we told the shell to execute the program `echo` with the argument `hello`. The `echo` program simply prints out its arguments. The shell parses the command by splitting it by whitespace, and then runs the program indicated by the first word, supplying each subsequent word as an argument that the program can access. If you want to provide an argument that contains spaces or other special characters (e.g., a directory named "My Photos"), you can either quote the argument with `'` or `"` (`"My Photos"`), or escape just the relevant characters with `\` (`My\ Photos`).

But how does the shell know how to find the `date` or `echo` programs? Well, the shell is a programming environment, just like Python or Ruby, and so it has variables, conditionals, loops, and functions. When you run commands in your shell, you are really writing a small bit of code that your shell interprets. If the shell is asked to execute a command that doesn't match one of its programming keywords, it consults an _environment variable_ called `$PATH` that lists which directories the shell should search for programs when it is given a command:

```console
missing:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
missing:~$ which echo
/bin/echo
missing:~$ /bin/echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

When we run the `echo` command, the shell sees that it should execute the program `echo`, and then searches through the `:`-separated list of directories in `$PATH` for a file by that name. When it finds it, it runs it (assuming the file is _executable_; more on that later). We can find out which file is executed for a given program name using the `which` program. We can also bypass `$PATH` entirely by giving the _path_ to the file we want to execute.

**Note:** You can use `Ctrl+C` to terminate a running shell process.

## Navigating in the shell

A path on the shell is a delimited list of directories; separated by `/` on Linux and macOS and `\` on Windows. On Linux and macOS, the path `/` is the "root" of the file system, under which all directories and files lie, whereas on Windows there is one root for each disk partition (e.g., `C:\`). We will generally assume that you are using a Linux filesystem in this class. A path that starts with `/` is called an _absolute_ path. Any other path is a _relative_ path. Relative paths are relative to the current working directory, which we can see with the `pwd` command and change with the `cd` command. `cd` can be run without any arguments to return to the home directory, and with an argument with the syntax `cd [DIRECTORY]` to move to another directory. In a path, `.` refers to the current directory, and `..` to its parent directory:

```console
missing:~$ pwd
/home/missing
missing:~$ cd /home
missing:/home$ pwd
/home
missing:/home$ cd ..
missing:/$ pwd
/
missing:/$ cd ./home
missing:/home$ pwd
/home
missing:/home$ cd missing
missing:~$ pwd
/home/missing
missing:~$ ../../bin/echo hello
hello
```

Notice that our shell prompt kept us informed about what our current working directory was. You can configure your prompt to show you all sorts of useful information, which we will cover in a later lecture.

In general, when we run a program, it will operate in the current directory unless we tell it otherwise. For example, it will usually search for files there, and create new files there if it needs to.

To see what lives in a given directory, we use the `ls` command:

```console
missing:~$ ls
missing:~$ cd ..
missing:/home$ ls
missing
missing:/home$ cd ..
missing:/$ ls
bin
boot
dev
etc
home
...
```

Unless a directory is given as its first argument, `ls` will print the contents of the current directory. Most commands accept flags and options (flags with values) that start with `-` to modify their behavior. Usually, running a program with the `-h` or `--help` flag will print some help text that tells you what flags and options are available. For example, `ls --help` tells us:

```
  -l                         use a long listing format
```

```console
missing:~$ ls -l /home
drwxr-xr-x 1 missing  users  4096 Jun 15  2019 missing
```

This gives us a bunch more information about each file or directory present. First, the `d` at the beginning of the line tells us that `missing` is a directory. Then follow three groups of three characters (`rwx`). These indicate what permissions the owner of the file (`missing`), the owning group (`users`), and everyone else respectively have on the relevant item. A `-` indicates that the given principal does not have the given permission. Above, only the owner is allowed to modify (`w`) the `missing` directory (i.e., add/remove files in it). To enter a directory, a user must have "search" (represented by "execute": `x`) permissions on that directory (and its parents). To list its contents, a user must have read (`r`) permissions on that directory. For files, the permissions are as you would expect. Notice that nearly all the files in `/bin` have the `x` permission set for the last group, "everyone else", so that anyone can execute those programs.

Some other handy programs to know about at this point are `mv` (to rename/move a file), `cp` (to copy a file), and `mkdir` (to make a new directory).

If you ever want _more_ information about a program's arguments, inputs, outputs, or how it works in general, give the `man` program a try. It takes as an argument the name of a program, and shows you its _manual page_. Press `q` to exit.

```console
missing:~$ man ls
```

**Note:** You can use `clear` to clear the terminal window.

## Cat

```console
missing:~$ cat /etc/hostname
```

Demonstrated in the example above, `cat` is a program that con`cat`enates files. When given file names as arguments, it prints the contents of each of the files in sequence to its output stream.

Regarding input/output streams, we will go into more detail on how to control and interact with these in later lectures on the linux shell.

## SSH

Secure shell (SSH) is a protocol used to log in to another computer over a network. The `ssh` tool is one of the most important utilities, as being able to use other computers without having to sit in front them is a key feature and something worth mastering. To log in to a remote machine with SSH, the command follows the format `ssh <username>@<host>`. This should prompt you for a password, and following authentication, drop you into a shell on the remote machine.

```bash
ssh abc123@server.net
# abc123@server.net's password:
# [abc123@server.net ~]$
```

## A versatile and powerful tool

On most Unix-like systems, one user is special: the "root" user. You may have seen it in the file listings above. The root user is above (almost) all access restrictions, and can create, read, update, and delete any file in the system. You will not usually log into your system as the root user though, since it's too easy to accidentally break something. Instead, you will be using the `sudo` command. As its name implies, it lets you "do" something "as su" (short for "super user", or "root"). When you get permission denied errors, it is usually because you need to do something as root. Though make sure you first double-check that you really want to do it that way!

**Note: Be careful when using `sudo`, make sure what you're running is safe, and you understand what is being done. If misused, root level privileges can damage and possibly even break your system.**

One thing you need to be root in order to do is writing to the `sysfs` file system mounted under `/sys`. `sysfs` exposes a number of kernel parameters as files, so that you can easily reconfigure the kernel on the fly without specialized tools. **Note that sysfs does not exist on Windows or macOS.**

For example, the brightness of your laptop's screen is exposed through a file called `brightness` under

```
/sys/class/backlight
```

By writing a value into that file, we can change the screen brightness.
An experienced shell user's first instinct might be to do something like:

```console
$ sudo find -L /sys/class/backlight -maxdepth 2 -name '*brightness*'
/sys/class/backlight/intel_backlight/brightness
$ cd /sys/class/backlight/intel_backlight/
$ sudo echo 3 > brightness
An error occurred while redirecting file 'brightness'
open: Permission denied
```

This error may come as a surprise. After all, we ran the command with `sudo`! This is an important thing to know about the shell. Operations like `|`, `>`, and `<` are done _by the shell_, not by the individual program. `echo` and friends do not "know" about `|`. They just read from their input and write to their output, whatever it may be. In the case above, the _shell_ (which is authenticated just as your user) tries to open the brightness file for writing, before setting that as `sudo echo`'s output, but is prevented from doing so since the shell does not run as root. Using this knowledge, we can work around this:

```console
$ echo 3 | sudo tee brightness
```

Since the `tee` program is the one to open the `/sys` file for writing, and _it_ is running as `root`, the permissions all work out. You can control all sorts of fun and useful things through `/sys`, such as the state of various system LEDs (your path might be different):

```console
$ echo 0 | sudo tee /sys/class/leds/tpacpi::lid_logo_dot/brightness
```

# Next steps

At this point you know your way around a shell enough to accomplish basic tasks. You should be able to navigate around to find files of interest and use the basic functionality of most programs. In the next lecture, we will talk about how to perform and automate more complex tasks using the shell and the many handy command-line programs out there.

# Exercises

Most classes in this course are accompanied by a series of exercises. Some give you a specific task to do, while others are open-ended, like "try using X and Y programs". We highly encourage you to try them out.

We have not written solutions for the exercises. If you are stuck on anything in particular, feel free to send us an email describing what you've tried so far, and we will try to help you out.

1.  For this course, you need to be using a Unix shell like Bash or ZSH. If you are on Linux or macOS, you don't have to do anything special. If you are on Windows, you need to make sure you are not running cmd.exe or PowerShell; you can use [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/) or a Linux virtual machine to use Unix-style command-line tools. To make sure you're running an appropriate shell, you can try the command `echo $SHELL`. If it says something like `/bin/bash` or `/usr/bin/zsh`, that means you're running the right program.
1.  Create a new directory called `missing` under `/tmp`.
1.  Look up the `touch` program. The `man` program is your friend.
1.  Use `touch` to create a new file called `semester` in `missing`.
1.  Write the following into that file, one line at a time:
    ```
    #!/bin/sh
    curl --head --silent https://missing.csail.mit.edu
    ```
    The first line might be tricky to get working. It's helpful to know that `#` starts a comment in Bash, and `!` has a special meaning even within double-quoted (`"`) strings. Bash treats single-quoted strings (`'`) differently: they will do the trick in this case. See the Bash [quoting](https://www.gnu.org/software/bash/manual/html_node/Quoting.html) manual page for more information.
1.  Try to execute the file, i.e. type the path to the script (`./semester`) into your shell and press enter. Understand why it doesn't work by consulting the output of `ls` (hint: look at the permission bits of the file).
1.  Run the command by explicitly starting the `sh` interpreter, and giving it the file `semester` as the first argument, i.e. `sh semester`. Why does this work, while `./semester` didn't?
1.  Look up the `chmod` program (e.g. use `man chmod`).
1.  Use `chmod` to make it possible to run the command `./semester` rather than having to type `sh semester`. How does your shell know that the file is supposed to be interpreted using `sh`? See this page on the [shebang](<https://en.wikipedia.org/wiki/Shebang_(Unix)>) line for more information.
1.  Use `|` and `>` to write the "last modified" date output by `semester` into a file called `last-modified.txt` in your home directory.
1.  Write a command that reads out your laptop battery's power level or your desktop machine's CPU temperature from `/sys`. Note: if you're a macOS user, your OS doesn't have sysfs, so you can skip this exercise.

# Feedback

As described before, feel free to fill our feedback [feedback form](https://forms.gle/EqEZwGWX4BsY7TFt8).
As bonus, we can also now generate a qr-code using the qrencode command line utility. While this utility is not installed by default (check our later sessions to learn how to install packets), you can give it a try and see if your distribution supports it:

```
$ echo "https://forms.gle/EqEZwGWX4BsY7TFt8" | qrencode -t ansiutf8
█████████████████████████████████████
█████████████████████████████████████
████ ▄▄▄▄▄ █▀█ █▄ ▀ █▀█▄▄█ ▄▄▄▄▄ ████
████ █   █ █▀▀▀█ ▄▀████ ▀█ █   █ ████
████ █▄▄▄█ █▀ █▀▀██ █▀▄█ █ █▄▄▄█ ████
████▄▄▄▄▄▄▄█▄▀ ▀▄█ ▀▄█▄█ █▄▄▄▄▄▄▄████
████▄▄  ▄█▄▄ ▄▀▄▀▀▀█▄███▀▄▀ ▀▄█▄▀████
█████  █▀█▄▀██▄█▀ ▄ ▀▄██▄▄▀ ▄▀█▀█████
████▀██▀  ▄█ ▄▄█▄█▄▄ ▀█▀  ▀▀▀▄▄█▀████
████▀▄██▄▀▄██   ▄█▀▄▀█ █ ▀ █▀▄▄▀█████
████▀█▄▄ █▄ ▄ ▄▄▀▀▀ ▀▄▄█▀▀▀ ▀▄ █▀████
████ ██   ▄▄ ▄██▀ ▄ ▀█▀▀ █▀ ██▄▀█████
████▄█▄▄▄▄▄▄▀▄▀█▄█▄  █▀▄ ▄▄▄ ▀   ████
████ ▄▄▄▄▄ █▄▄▄ ▄█▀▄ ▄ ▄ █▄█ ▄▄▀█████
████ █   █ █ ▀█▄▀▀▀▄▄▄█▀▄▄▄▄▄▀ ▀▀████
████ █▄▄▄█ █ ▀ █▀ ▄ ▄▄▄▄▀▄ ▄▄ ▄ █████
████▄▄▄▄▄▄▄█▄▄██▄█▄█▄██▄█▄█▄▄█▄██████
█████████████████████████████████████
█████████████████████████████████████
```
