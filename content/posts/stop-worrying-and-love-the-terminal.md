---
title: "How I Learned to Stop Worrying and Love the Terminal"
date: 2024-02-17T14:45:25+01:00
draft: true
tags:
  - Terminal
  - Tools
---

This post is a reflection on how how my view of the terminal changed from
intimidating and esoteric to `$HOME` sweet `$HOME`. The terminal has become an
incrediby productive tool for myself, that I use all the time. The reasons why
you would want to use a terminal instead of GUI-based tools are many, including

- The ability to automate repetetive tasks
- Fast access to all programs on your computer
- Many GUIs for tools like `git`, are missing features that are available at the
  command line
- Full customizability. You can create the perfect tool for you
- A mouse-free workflow. Once you cut the cord you will notice how clumsy it is
  for most tasks
- Compared to using an IDE, you will gain a better understanding of how your
  environment works

I'm going to talk about my history with the termial, what key insights helped me
gain a better understanding of Linux, as well as some of my favourite
command-line tools and hacks.

## My terminal history

I was always a Windows defender, having used it since I was a child, mostly to
play games. I had dabbled a little with Java wanting to make the next Minecraft,
but with little success. During that time, I had occasionally opened CMD, mostly
by accident, but it was always promptly closed.

It was first when I started university that I encountered Linux, and Linux fan
boys for the first time. Out of the people I talked to on my first day, everyone
seemed to only want to talk about their favourite distributions, and what the
benefits of Ubuntu were compared to Red Hat. I thought they were crazy.
Thankfully I found a circle of friends who didn't care about Linux either.

My first real experience with the terminal was a short Linux introduction course
the first couple of weeks of university. We learned that `cd` changes the
current directory, `mv` and `cp` moved and copied files around and lastly that
we could use `emacs` to edit text files. It all seemed like a convoluted file
explorer. I didn't get the point. There were so many commands with loads of
options and the `man`-pages just made me more confused. If I ever needed to edit
text files, I could just use notepad (oof, I know...).

A few years later I took a course in high-performance computing as part of my
masters. The course had just become mandatory for a couple of popular masters
programs and Big Data (TM) was all the rage. The course had gone from ~30
dedicated students the year prior, to over 150 students, most of whom had never
touched a compiler, myself included. It was evident that the professor was not
very pleased.

In the course we used C on a remote machine where we could not install our own
software, leaving little room for anything other than a 100% terminal-based
workflow, and it was rough. I was lucky enough to team up with an acquaintance
with more Linux experience, which was a saving grace, and I ended up learning a
great deal. Again, we used `emacs` for file editing and we `tmux` to emulate
several terminals within the same window, so that we could edit the code and run
the compiler side-by-side. We also used a little program called git to cooperate
on the code.

It was only when I started working my first job after university that I started
using the terminal more frequently. We were working on a small deployment tool
based on docker that we developed through WSL (Windows Subsystem Linux). I
mostly ran commands in the integrated terminal in VSCode, like tests and
linters, docker, and basic git.

Over time I started to become quite comfortable in the Linux ecosystem inside
the little VM that is WSL. I understood now what the Linux fan boys where
talking about, and I wanted to dive deeper. Since a while back I have solely
been using Linux at work and I intend to keep it that way.

## The enlightenment

There were a number of insights that made a large difference in my understanding
of the terminal and Linux in general. I still think the terminal more or less an
advanced file explorer, which is perfect, because almost everying in Linux is a
file. The commands, like `ls` and `cd` are simply executable files that exist in
a directory where Linux knows to look for programs. These directories are found
in an _environment variable_ called `$PATH`.

Environment variables are tied to the process an application is running on and
can be accessed with `$VAR` in your shell. You can set environment variables for
the _current_ session with `export VAR=value` and you can see all environment
variables with `printenv`. The exported environment variable will be gone next
time you start a terminal. To make it persistent, you need to add the export
statement to `.bashrc` or `.profile` in your home directory. These files are run
every time you start a new terminal, so the environment variable will always be
set.

Every user on a Linux machine has a username and one or more groups. Permissions
can be set so that only certain groups or users can read, write or execute
certain files. Many commands and files outside of your home directory can only
be accessed by the _root_ user. You can use `sudo <command>` to run a single
command as if you were the root user.

Almost every Linux distribution will have a package manager that you can use to
install programs easily from the command line (or with a GUI). In my opinion,
these package managers are one of the main benefits of using Linux over other
operating systems. You will rarely need to visit third party websites to install
new programs. In addition, the package manager handles your updates and often
they will run tests to make sure that the package versions work together.

In Debian-based distros, like Ubuntu, you have the `apt` package manager. To
install a program you simply type `sudo apt install firefox` and then start it
with `firefox`. You can uninstall and remove related files with `sudo apt purge`
to avoid the bloat that is commonly left behind uninstall Windows programs.

Part of the [Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy)
says that you should write programs that work together. In a shell, this becomes
much easier than in graphical applications, since every program uses text both
as input and as output. This allows us to chain commands together, using the
output of one tool as the input to the next until we get our final result. This
is called _piping_.

> TODO! ^

Finally, it's useful to be familiar with the Linux file system. The file system
is structured like a tree, where the root directory is called `/`. The
directories you will most often interact is your `$HOME` directory, also called
`~`, located at `/home/username`, this is where all of your user's private files
are stored. Other directories that are good to know are

- `/usr/bin`: Contains system-wide executables
- `/etc`: Contains system-wide configurations
- `/mnt`: Contains mounted storage, like hard drives

> I should still mention

- Piping | >
- Common shortcuts, CTRL-C, CTRL-D, q

## Unlocking the productivity

> This text is bad v

As much as I enjoy working in the terminal, there are still issues. Fortunately
Linux enthusiasts embrace the mantra sharing is caring, and for most issues
there exist tools that someone has created and shared with the world.

### Discoverability

Discovering what's possible and how to do it might be the biggest hurdles to get
over when learning Linux. Many commands will have a `man`-page, which is a
manual that can be accessed with `man <command>`. When I started out I thought
these manuals were very hard to read, but they have become more helpful over
time. Another option is to use the `--help` flag that exists for most commands
that I've found often gives more digestible information.

I want to highlight a useful tool called [tldr](https://tldr.sh/) (too long
didn't read), which is a community- driven effort to create tiny cheat-sheets
for common command-line tools. For example, `tldr tar` will show a list of
common ways to use the `tar` command with simple explanations of what the
commands do. Below is the first couple of examples:

```
- [c]reate an archive and write it to a [f]ile:
    tar cf path/to/target.tar path/to/file1 path/to/file2 ...

- [c]reate a g[z]ipped archive and write it to a [f]ile:
    tar czf path/to/target.tar.gz path/to/file1 path/to/file2 ...
```

### Shell history

Your shell keeps a history of the commands you've run recently. You probably
know that you can press the up-arrow to go to the most recent commands, but by
pressing CTRL-R you are able to search your shell history to find commands you
ran months ago. This is really useful when you know you've run a command before,
but you cannot remember the exact options, or you just want to save keystrokes
running a common command.

You can supercharge the shell history search with a nice interface and fuzzy
search with [fzf](https://github.com/junegunn/fzf), which I cannot recommend
enough. During installation it will automatically replace CTRL-R to use fzf
instead of the default search. But fzf can do much more than that! Personally, I
use it to search for any directory and automatically `cd` there, list `tmux`
sessions to attach to, and git branches to checkout.

If you find yourself reaching for the same command over and over you may want to
create an `alias` for it. For example, I have created a large number of aliases
for the git commands I run most often. I recommend that you dedicate an area of
your `.bashrc` for all of your aliases. Here are some of my most frequently used
git aliases

```sh
# Aliases
alias gco='git checkout'
alias gcob='git checkout -b'
alias gc='git commit'
alias gcm='git commit -m'
alias gs='git status -s'
alias gl='git log'
alias gpl='git pull'
alias gps='git push'
alias gpssu='git push --set-upstream origin $(git rev-parse --abbrev-ref HEAD)'
```

### Searching and finding

It's really worthwhile becomming familiar with `grep` and `find`. From the
man-page say that `grep` will "print lines that match patterns", and it really
is that simple. A very common usecase is to search a log file for some
information, or to find lines in a man-page that mentions a certain word. For
example, to quickly check if there is an option to _size_ for `ls` you could run
`man ls | grep size`, which pipes the output of `man ls` to `grep size` to only
print the lines where _size_ is mentioned.

```
--block-size=SIZE
       with -l, scale sizes by SIZE when printing them; e.g., '--block-size=M'; see SIZE format below
       with -l and -s, print sizes like 1K 234M 2G etc.
-s, --size
       print the allocated size of each file, in blocks
-S     sort by file size, largest first
       sort by WORD instead of name: none (-U), size (-S), time (-t), version (-v), extension (-X)
-T, --tabsize=COLS
```

`find` on the other hand is used to "search for files in a directory hierarchy",
according to the manpage. Sometimes you may find that you do not know where you
put a file, and `find` can help you find it. To search for a file with a certain
name you could use `find . -name 'filename'` and find will recursively go
through all directories and print every file it finds with a name that matches
the given pattern. You could even pipe the result to `fzf` if there are many
matches!

`find` and `grep` can sometimes be a bit slow, and if you often find yourself
waiting for these tools, it might be worthwhile to installtheir modern
alternatives `ripgrep` for `grep` and `fd` for `find`.

### Multi-tasking

> What I want to talk about

- tmux
- backgrounding tasks
