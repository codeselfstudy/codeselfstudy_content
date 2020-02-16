---
title: Bash One-Liner: Search for Multiple Files and Open in Vim Tabs
date: 2017-02-22
author: Josh
path: "/blog/bash-one-liner-search-for-multiple-files-and-open-in-vim-tabs/"
---

I was looking for a group of <code>.desktop</code> files on Ubuntu. I wanted to examine the contents after finding them. I discovered a nice command line trick along the way.

To find <code>.desktop</code> files, you can run these commands in a shell:

```bash
sudo updatedb
locate *.desktop
```

That will print out a long list of files. I wanted to limit them to ones related to Vim:

```bash
locate *.desktop | grep -i vim
```

(<code>grep -i vim</code> means search for files that contain the string "vim", case insensitive. The pipe character (<code>|</code>) takes the output of the previous command and pipes it into the next command. So the output of <code>locate *.desktop</code>, which is a long list of files, gets piped into <code>grep -i vim</code>, which returns only the files that contain the string "vim" somewhere inside.)

It's easy to loop over files in the terminal like this, creating a list of target files inside of the command substitution section indicated by <code>$()</code>:

```bash
for f in $(locate *.desktop | grep -i vim)
do
    echo "The file can be manipulated on this line of code. Current file: $f"
done
```

It's possible to search for load the target files into Vim tabs where they can be viewed easily (<code>gt</code> or <code>gT</code> to switch tabs) like this:

```bash
vim -p $(locate *.desktop | grep -i vim)
```

(The <code>-p</code> option tells Vim to open the files in tabs.)

It's a nice way to search for and load several files at once in one line, so I thought I would share it here.
