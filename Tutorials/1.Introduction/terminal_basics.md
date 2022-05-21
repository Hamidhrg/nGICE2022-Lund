<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Basics of using a terminal](#basics-of-using-a-terminal)
    - [A general introduction](#a-general-introduction)
        - [Windows users](#windows-users)
        - [Mac and Linux users](#mac-and-linux-users)
    - [Navigating around the filesystem](#navigating-around-the-filesystem)
        - [Where am I?](#where-am-i)
        - [Listing contents of a directory](#listing-contents-of-a-directory)
        - [Navigating into a directory](#navigating-into-a-directory)
        - [Printing stuff to the screen](#printing-stuff-to-the-screen)
        - [Creating files](#creating-files)

<!-- markdown-toc end -->

# Basics of using a terminal

## A general introduction

To be able to follow the practical tutorials of this workshop, you will need to get familiarized with using the command-line. But first let me start with a set of very brief definitions of some of the terms you will hear. What are the terms "command-line", "terminal", "shell", "bash", "linux", "UNIX" ?? I will try to explain them in no particular order.

First, linux and UNIX. `UNIX` is a an operating system that was developed in the 80's at Bell Laboratories. At the time it was revolutionary regarding how much it changed how people use computers, in both personal use and commercial and research use at universities. Eventually, different versions of it spun off, or in some cases, entirely new "functionally equivalent" copies were created without using unix code at all. Some came out to be the core of the operating system you use on your Macs today and some are what is collectively known as "Linux". An OS that vast majority of commercial computer servers, cloud providers and research computation facilities use.

In a unix-like system *shell* is a program that provides a way of interacting with the operating system that is different than what we are used in our day to day computer use. A *terminal*, or to use a more techincally correct term, a *terminal emulator* is another program in your OS that runs that *shell* and lastly *bash* is one of the most commonly used shells and also comes as default for many unix-like systems. The way you can use a terminal is what is know as a *command-line interface*, or *CLI* for short. We will have practical examples soon to demonstrate these to you.

MacOS and Linux systems have the functionality we will use today natively, but windows does not. Because of that, we arranged a linux server for all of you to use during this workshop. This way we can be sure you are using the same exact system and diagnose any problems you had during tutorials more easily. It also has all the command-line phylogenetic and bioinformatic programs you will need installed. So before learning how to use the terminal, I need to quickly show you how to connect to the server.

But for now, during the very basic introduction to using the shell, Mac users can remain on their own computers if they want to experiment a little bit or can come with us and log in to the server.


### Windows users

Launch the `MobaXterm` application. At the top left corner of the window click on the icon that is labelled "session" and choose "ssh" when asked. In the ip address field enter the ip address that is presented to you in the classroom. For user enter "workshop" without quotes. The required password will be given out in-class as well.


### Mac and Linux users

Launch your "Terminal" app. Type the following command and hit return/enter

```bash
ssh workshop@ip.adress.of.server
```

you will replace the part after the `@` sign with the actual IP address you are presented in-class.


## Navigating around the filesystem


### Where am I?

Usually, when you log in to (or start a terminal session on ) a unix-like system, you will be in your *home directory*. This is your user's main folder. Let's assume your username is `theuser`. For Linux this will be `/home/theuser`, and for MacOS `/Users/theuser`.

Let's check this. To find out your current location in a filesystem when in a terminal you can run the `pwd` (print working directory) command.

If you are on the server, you should see `/home/workshop` as the output.


### Listing contents of a directory

You are now different instances of the same user `workshop` on this machine. Since it was easier for us to manage this workshop this way, we only created a single user, but we created sub-folder for each of you participants under the user `workshop` s home directory.

Let's check that.

To list the contents of the current directory you are in, you can run the `ls` command (short for list). You should see the single word `Users` as the output. All of your dedicated folders are under this directory.


### Navigating into a directory

Now, we know how to list a directory we are currently in, and print out where that directory located in, but how can we go the `Users` directory so that we can run `ls` once again to check if our name appears in one of the listed directories there?

To change the current directory we are in, we can use the `cd` command. Without any additional information, this command will take you to your current user's home directory (`/home/workshop`) which is where we currently are. Doesn't seem really useful..

But, it is possible to give an *argument* to this command. In bash, we can assume that any text separated by a space is an additional argument to the command or program that it comes after. Like:

```bash
program argument1 argument2
```

And `cd` takes a location in your filesystem (we will call this a *path* from now on) as an argument to take you that location. So let's check what happens if we give it the directory name *Users* . And after that run commands `pwd` and `ls` command once again.

Run these 3 commands in order:

```bash
cd Users
pwd
ls
```

Now, you should see about 15 different names including Hamid, Etka, and your names. Theses directories will hold all of your files during the workshop. Let's use `cd` once more (with your folder's name as the argument) and go to our dedicated directories.


### Printing stuff to the screen

It won't seem so useful to learn this in isolation, but it is important that you know how to print stuff to the screen with various commands for different applications.

The easiest way to print something to the screen is to use the `echo` command.

Try this:

```bash
echo "Bash is awesome!"
```

    Bash is awesome!


### Creating files

What if we want to say things but keep those in a file stored safely, rather than seeing the output on the screen and losing it afterwards?

Its actually really easy to do! Try this:

```bash
echo "Bash is awesome!" > my_words.txt
```

now, you shouldn't see anything on the screen. Check the contents of your directory again, you will see a new file named `my_words.txt`. Cool!

What we just did, is called **redirection** in shell jargon. In particular, we redirected the **standard output** to a file, instead of its current location, our terminal screens. But how can we sure our words were written to the newly created file?

We need to check the contents of that file. Among other things, you can use the `cat` command to print out everyting written to a file, but this command is actually for con-**cat**-enating several files. But giving it a single file name also works!

Let's try:

```bash
cat my_words.txt
```

    Bash is awesome!

If you don't want to create a new file to write to (or overwrite the existing one), you can use double greater-than-signs instead of the single we used above. This will append new lines to the existing file.

Let's try adding more lines to the existing file:

```bash
echo "It can also append to files." >> my_words.txt
```

and check its contents once again:

```bash
cat my_words.txt
```

    Bash is awesome!
    It can also append to files.
