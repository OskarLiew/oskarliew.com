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
you would want to use a terminal instead of GUI-based tools are many.

<!--more-->

- The ability to automate repetetive tasks
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
play games. I had dabbled a little with Java, wanting to make the next
Minecraft, but with little success. During that time, I had occasionally opened
CMD, mostly by accident, but it was always promptly closed.

It was first when I started university that I encountered Linux, and Linux fan
boys, for the first time. Out of the people I talked to on my first day,
everyone seemed to only want to talk about their favourite distributions and
what the benefits of Ubuntu were compared to Red Hat. I thought they were crazy.
Thankfully I found a circle of friends who didn't care about Linux either.

Soon after we had a Linux introduction course. We learned that `cd` changes the
current directory (Linux for folder), `mv` and `cp` moved and copied files
around and lastly that we could use `emacs` to edit text files. It all seemed
like a convoluted file explorer. I still didn't get the point. There were so
many commands with loads of options and the `man`-pages just made me more
confused. If I ever needed to edit text files, I could just use notepad (oof, I
know...).

A few years later I took a course in high-performance computing as part of my
masters. The course had just become mandatory for a couple of popular masters
programs and Big Data (TM) was all the rage. The course had gone from ~30
dedicated students the year prior, to over 150 students, most of whom had never
touched a compiler, myself included. It was evident that the professor was not
very pleased.

In the course we used C on a remote machine where we could not install our own
software, leaving little room for anything other than a 100% terminal-based
workflow, and it was rough. I was lucky enough to team up with an acquaintance
with more Linux experience, and I ended up learning a great deal. Again, we used
`emacs` for file editing and we used `tmux` to emulate several terminals inside
the same window, so that we could edit the code and run the compiler
side-by-side. We also used a little program called git to cooperate on the code.

It was first after I started my first job after university that the terminal
became a core tool in my arsenal. We were working on a small deployment tool
based on docker that we developed through WSL (Windows Subsystem Linux). I
mostly ran commands in the integrated terminal in VSCode, like tests and
linters, docker, and basic git.

Over time I started to become quite comfortable in the Linux ecosystem inside
the little VM that is WSL. I understood now what the Linux fan boys were talking
about, and I wanted to dive deeper. For a while now, I have solely been using
Linux at work and I intend to keep it that way.

## The enlightenment

There were a number of insights that made a large difference in my understanding
of the terminal and Linux in general. I still think of the terminal more or less
as an advanced file explorer, which is perfect, because almost everying in Linux
is a file. The commands, like `ls` and `cd` are simply executable files that
exist in a directory where Linux knows to look for programs. These directories
are found in an _environment variable_ called `$PATH`.

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
command as if you were the root user. Do this with caution, however, since you
might expose vurnerabilities or even break your system if you are not careful.

Almost every Linux distribution will have a package manager that you can use to
install programs easily from the command line (or with a GUI). In my opinion,
these package managers are one of the main benefits that Linux offers over other
operating systems. You will rarely need to visit third party websites to install
new programs. In addition, the package manager handles your updates and the
programs are tested so you can be confident that the packages will work
together.

On Debian-based distros, like Ubuntu, you have the `apt` package manager. To
install a program you simply type `sudo apt install firefox` and then start it
with `firefox`. You can uninstall and remove related files with
`sudo apt purge`. Doing it this way will avoid the bloat that is commonly left
behind uninstalled Windows programs.

One part of the [Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy)
states that programs should be written to work together. In a shell, combining
tools is much easier than in graphical applications, since every program uses
text as both input and output. This allows us to chain commands together, using
the output of one tool as the input to the next until we get our final result.
This is called _piping_ and is achieved with the `|` character. Piping is an
incredibly powerful mechanism for combining tools and automating processes that
would otherwise take several commands.

Programs that are run on the command line have three data streams connected to
them.

- STDIN (0) - Standard input. The data that is fed into the program
- STDOUT (1) - Standard output. The data that output by the program into the
  terminal
- STDERR (2) - Standard error. Error messages, also outputs to the terminal

Piping is one way in which the streams of different programs can be combined
together. Another mechanism is _redirection_, that is able to take the output
from one stream and send it to another. To redirect STDOUT to a file you use the
`>` character. `man ls > ls-manual.txt` will create a text file with the
contents of the `ls` manual. Redirecting another command's output to the same
file will overwrite its contents, but you can append instead with `>>`.

Finally, it's useful to be familiar with the Linux file system. The file system
is structured like a tree, where the root directory is called `/`. The directory
you will most often interact is your `$HOME` directory, located at
`/home/username`, this is where all of your private files are stored. The tilde
`~` character can be used as a shorthand for the home directory. Other
directories that are good to know are

- `/usr/bin`: Contains system-wide executables
- `/etc`: Contains system-wide configurations
- `/mnt`: Contains mounted storage, like hard drives

## Unlocking the productivity

The command-line takes a little bit getting used to and there are many things to
learn. However, once you're armed with the insights listed above, and
comfortable navigating the file-system and editing files, I believe the biggest
hurdles are behind you. Now you're ready to get to the good parts, namely
supercharging your productivity!

### Discoverability

Discovering what's possible and how to do it, can be tricky. Many commands will
have a `man`-page, which is a manual that can be accessed with `man <command>`.
When I started out I thought these manuals were very hard to read, but they have
become more helpful over time. Another option is to use the `--help` flag that
exists for most commands that I've found often gives more digestible
information.

I want to highlight a useful tool called [tldr](https://tldr.sh/) (too long
didn't read), which is a community-driven effort to create tiny cheat-sheets for
common command-line tools. For example, `tldr tar` will show a list of common
ways to use the `tar` command with simple explanations of what the commands do.
Below is the first couple of examples:

```
- [c]reate an archive and write it to a [f]ile:
    tar cf path/to/target.tar path/to/file1 path/to/file2 ...

- [c]reate a g[z]ipped archive and write it to a [f]ile:
    tar czf path/to/target.tar.gz path/to/file1 path/to/file2 ...
```

### Shell history

Your shell keeps a history of the commands you've run recently. You probably
know that by pressing the up-arrow to you can navigate your recent commands but
this quickly becomes annoying. By pressing CTRL-R you are able to search your
shell history to find commands you ran months ago. This is really useful when
you know you've run a command before, but you cannot remember the exact options,
or to save keystrokes running a common command.

You can supercharge the shell history search with a nice interface and fuzzy
search with [fzf](https://github.com/junegunn/fzf), which I cannot recommend
enough. During installation it will automatically replace CTRL-R to use fzf
instead of the default search. But fzf can do much more than that! Personally, I
use it to search `$HOME` to `cd` to far-away directories, list `tmux` sessions
to attach to, and git branches to checkout.

### Aliases

You will probably find yourself reaching for the same command over and over, and
then it is a good idea to create an `alias` for it. For example, I have a large
number of aliases for the git commands I run most often, listed below. I
recommend that you dedicate an area of your `.bashrc` to put aliases.

```sh
# Git aliases
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

I strongly recommend that you familiarize yourself with `grep` and `find`. From
the man-page of `grep` we learn that it "prints lines that match patterns" and
while it sounds simple, it's incredibly useful. A very common usecase is to
search a log file for some information or to find lines in a man-page that
mentions a certain word. For example, to quickly check if there is an option to
see the _size_ of a file with `ls` you could run `man ls | grep size`, which
pipes the output of `man ls` to `grep size` to only print the lines where _size_
is mentioned.

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

`find`, on the other hand, is used to "search for files in a directory
hierarchy", according to the man-page. Sometimes you may find that you do not
know where a file is located, and that's when you'd use `find`. To search for a
file with a certain name you could use `find . -name 'filename'` and find will
recursively go through all directories and print every file it finds with a name
that matches the given pattern. You could even pipe the result to `fzf` if there
are many matches!

`find` and `grep` can sometimes be a bit slow and if you find yourself waiting
for these tools often, it might be worthwhile to install their modern
alternatives `ripgrep` for `grep` and `fd` for `find`.

### Multi-tasking

I've mentioned `tmux` in passing, but it has recently become one of my favourite
programs for productivity on the command line. Tmux stands for _terminal
multiplexer_ and is a way to emulate several terminals within a single window.
You can start a session by running `tmux`, which will give you a green bar at
the bottom of the screen, indicating that it is active. I use tmux constantly,
and without it I feel naked. I've found that it is especially useful when I have
long-running tasks, like deep learning model training, that I want to have in
the background and not risk terminating prematurely. I can simply detach from
the session, and even if I close the terminal window I can be confident it's
still going. It's also really useful when you are working on several projects at
once, since you can easily jump between sessions to switch context. You can even
script tmux so you can start up or attach to your development environment with a
single command.

The keybindings for tmux are not the most intuitive, so when starting out I
would recommend this [cheat sheet](https://tmuxcheatsheet.com/). By default, all
tmux keybindings are prefixed with CTRL-B and followed by another keypress. Here
are my top 10 most useful tmux commands

- `%` - Split the window with a vertical line
- `"` - Split the window with a horizontal line
- `arrow-key` - Change focus to the pane in the arrow-key direction
- `CTRL` + `arrow-key` - Resize pane in arrow-key direction
- `x` - Close focused pane
- `d` - Detach from session. It will still run in the background. List all
  sessions with `tmux list-sessions` and attach to an existing session with
  `tmux attach -t <target-session>`
- `c` - Create a new window in the current session
- `0` ... `9` - Select window by number
- `s` - Open session selector
- `[` - Enter copy-mode. In copy mode: `q` to quit, `Spacebar` to start
  selection and `Enter` to copy selection

If you think tmux might be useful for you I cannot recommend this amazing
mini-course by [Chris Toomey](https://thoughtbot.com/upcase/tmux) enough. Follow
it and you wil end up with a really usable configuration.

The last tip I want to share is backgrounding processes. Let's say you've
started a long-running process, like a web server, that has taken over your
terminal session. You can move that process to the background by pressing CTRL-Z
and you will get back control of the terminal. You can foreground the process
again with `fg`. To start a command to be run in the background from the
beginning, you can add an `&` to the end of the command. Please note, however,
that this is different from detaching from a tmux session, since when you close
your terminal session with background tasks they will be terminated.

## Conclusion

There are many more things I would wish to mention, but I wanted to keep this
post at a level where you should be able to follow along even with only a tiny
amount of command-line experience. If you find yourself in that group of people
then I hope that I've learned something new and that you maybe you might be
willing to give life on the command life a try. I assure you, it can even be
quite `$HOME`-ey.

Despite being ancient technology by computing standards, it feels like the
terminal is going stronger than ever, with tons of new and exciting tools and
growing communities, like [r/unixporn](https://www.reddit.com/r/unixporn/)
pushing the boundaries of what's possible in a shell.

In the future I may write posts about more advanced topics, like alternative
shells and advanced customizations. But until then, happy hacking.
