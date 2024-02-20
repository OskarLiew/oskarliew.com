---
title: "How I Learned to Stop Worrying and Love the Terminal"
date: 2024-02-17T14:45:25+01:00
draft: true
tags:
  - Terminal
  - Tools
---

This post is a reflection on how how my view of the terminal changed from
intimidating and slightly esoteric to `$HOME` sweet `$HOME`. The terminal has
become an incrediby productive tool for myself. The reasons why you would want
to use a terminal instead of GUI-based tools are many, including

- The ability to automate repetetive tasks
- Fast access to all programs on your computer
- Many GUIs for tools like `git`, are missing features that are available at the
  command line
- Full customizability. You can create the perfect tool for you
- A mouse-free workflow. Once you cut the cord you will notice how clumsy it is
  for most tasks

I'm going to talk about my history with the termial, what key insights helped me
gain a better understanding of Linux, as well as some of my favourite
command-line tools and hacks.

## My terminal history

I was always a Windows defender, having used it since I was a child to play
games. I had dabbled a little bit with Java, wanting to make the next Minecraft.
I had occasionally opened CMD on windows, mostly by accident, and it was always
promptly closed.

It was first when I started university that I encountered Linux fan boys for the
first time. Out of the people I talked to on my first day, everyone seemed to
only want to talk about their favourite distributions, and what the benefits of
Ubuntu were compared to Red Hat. I thought they were crazy. Thankfully I found a
circle of friends who didn't care about Linux either.

My first real experience with the terminal was a short Linux introduction course
the first couple of weeks of university. We learned to `cd` to change directory,
`mv` and `cp` to move and copy files and lastly `emacs` to edit text files. It
all seemed like a convoluted file explorer. I didn't get the point. There were
so many commands with loads of options and the `man`-pages just made me more
confused, and to edit text files, I could just use notepad (oof, I know...).

Fast forward a few years, I took a course in high-performance computing as part
of my masters. The course had just become mandatory for a couple of popular
masters programs, and Big Data (TM) was all the rage. The course had gone from
~30 dedicated students the year prior, to over 150 students, most of whom had
never touched a compiler, myself included. It was evident that the professor was
not very pleased.

In the course we used C on a remote machine where we could not install our own
software, leaving little room for anything other than a 100% terminal-based
workflow, and it was rough. I was lucky enough to team up with an acquaintance
with more Linux experience, which was a saving grace, and I ended up learning a
great deal. Again, we used `emacs` for file editing and we used `tmux` to
emulate several terminals within the same window, so that we could edit the code
and run the compiler side-by-side. We also used a little program called git to
cooperate on the code.

It was only when I started working my first job after university that I started
using the terminal more frequently. We were working on a small deployment tool
based on docker that we used through WSL (Windows Subsystem Linux). I mostly ran
commands in the integrated terminal in VSCode, like tests and linters, docker,
and basic git.

Over time I started to become quite comfortable in the Linux ecosystem inside
the little VM that is WSL. I understood now what the Linux fan boys where
talking about, and I wanted to dive deeper. So a little under a year ago I
installed Arch Linux (BTW).

## The enlightenment

There were a number of insights that made a large difference in my understanding
of the terminal and Linux in general. Here are some of my key insights:

I still think the terminal more or less an advanced file explorer, and almost
everying in Linux is a file. The commands, like `ls` and `cd` are simply
executable files that exist in a directory where Linux knows to look for
programs. These directories are found in an _environment variable_ called
`$PATH`.

Environment variables are tied to the process an application is running on and
can be accessed with `$VAR`. You can set environment variables for the _current_
session with `export VAR=value` and you can see all environment variables with
`printenv`. The exported environment variable will be gone next time you start a
terminal. To make it persistent, you need to add the export statement to
`.bashrc` or `.profile` in your home directory. These files are run every time
you start a new terminal.

Every user on a Linux machine has a username and one or more groups. Permissions
can be set so that only certain groups or users can read, write or execute
certain files. Many commands and files outside of your home directory can only
be accessed by the `root` user. You can use `sudo <command>` to 'pretend' you
are root for a single command.

Almost every Linux distribution will have a package manager that you can use to
install programs easily from the command line. In my opinion, these package
managers, are one of the main benefits of using Linux over another OS. These
package managers will handle updating your programs and your system and you will
rarely need to visit a bunch of websites to download your favourite tools. In
Debian-based distros, like Ubuntu, you have the `apt` package manager. To
install a program you simply type `sudo apt install firefox` and then start it
with `firefox`. You can uninstall and remove related files with
`sudo apt purge`, avoiding the bloat that is commonly left behind uninstall
Windows programs.

It's useful to be familiar with the Linux file system. The file system is
structured like a tree, where the root directory is called `/`. The directories
you will most often interact is your `$HOME` directory, also called `~`, located
at `/home/username`, this is where all of your user's private files are stored.
Other directories that are good to know are

- `/usr/bin`: Contains system-wide executables
- `/etc`: Contains system-wide configurations
- `/mnt`: Contains mounted storage, like hard drives

## Unlocking the productivity
