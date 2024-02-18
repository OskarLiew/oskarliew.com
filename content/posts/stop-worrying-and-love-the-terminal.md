---
title: "How I Learned to Stop Worrying and Love the Terminal"
date: 2024-02-17T14:45:25+01:00
draft: true
tags:
  - Terminal
  - Tools
---

This post is a reflection on how how my view of the terminal changed from intimidating
and slightly esoteric to `$HOME` sweet `$HOME`, the most used application on my computer.
I'm going to talk about some of the key insights that helped gain a better understanding
of what's going on, as well as some of my favourite tools.

## My terminal history

> Mention the first day at uni?

In my youth I had occasionally opened CMD on windows, mostly by accident, but it was
always promptly closed. My first real experience of a temrinal was a short Linux
introduction course the first couple of weeks of university. We learned to `cd` to
change directory, `mv` and `cp` to move and copy files and lastly `emacs` to edit text
files. It all seemed like a convoluted file explorer. I didn't get the point. There were
so many commands with loads of options and the `man`-pages just made me more confused,
and to edit text files, I could just use just notepad (oof, I know...).

Fast forward a few years, I took a course in high-performance computing as part of my
masters. The course had just become mandatory for a couple of popular masters programs,
and Big Data (TM) was all the rage, so the course had gone from ~30 dedicated students
the year prior, to over 150 students, most of whom had never touched a compiled language.

In the course we used C on a remote machine where we could not install our own software,
leaving little room for anything other than a 100% terminal-based workflow, and it was
rough for most students, myself included. I was lucky enough to team up with an acquaintance
with more Linux experience, which was a saving grace, and I ended up learning a great
deal. Again, we used `emacs` for file editing and we started using `tmux` to emulate
several terminals within the same window.
