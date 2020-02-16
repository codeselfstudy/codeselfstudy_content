---
title: How to Remove All .elc Files (Emacs)
date: 2018-04-27
author: Josh
path: "/blog/how-to-remove-all-elc-files-emacs/"
---

When switching back to <a href="https://i3wm.org/">i3 window manager</a>, my Emacs stopped working. I kept getting the error below:

```text
Debugger entered--Lisp error: (void-function cl-struct-define)
cl-struct-define(evil-jumps-struct nil cl-structure-object nil nil ((cl-tag-slot) (ring) (idx -1)) cl-struct-evil-jumps-struct-tags cl-struct-evil-$
byte-code("\300\301\302\303#\210\304\305\306\307\306\211\310\311\312\303& \207" [function-put make-evil-jumps-struct side-effect-free t cl-struct-d$
require(evil-jumps)
byte-code("\300\301!\210\300\302!\210\300\303!\210\300\304!\210\300\305!\210\300\306!\210\300\307!\210\300\310!\210\300\311!\210\312\313\314\"\207"$
require(evil-commands)
byte-code("\300\301!\210\300\302!\210\300\303!\210\300\304!\210\300\305!\210\300\306!\210\300\307!\210\300\310!\210\300\311!\210\300\312!\210\300\3$
require(evil)
eval-buffer(#<buffer  *load*-997250> nil "/home/username/.emacs.d/configuration.el" nil t)  ; Reading at buffer position 3100
load-with-code-conversion("/home/username/.emacs.d/configuration.el" "/home/username/.emacs.d/configuration.el" nil nil)
load("/home/username/.emacs.d/configuration.el" nil nil t)
load-file("~/.emacs.d/configuration.el")
org-babel-load-file("~/.emacs.d/configuration.org")
eval-buffer(#<buffer  *load*> nil "/home/username/.emacs.d/init.el" nil t)  ; Reading at buffer position 408
load-with-code-conversion("/home/username/.emacs.d/init.el" "/home/username/.emacs.d/init.el" t t)
load("/home/username/.emacs.d/init" t t)
#[0 "^H\205\262^@ \306=\203^Q^@\307^H\310Q\202;^@ \311=\204^^^@\307^H\312Q\202;^@\313\307\314\315#\203*^@\316\202;^@\313\307\314\317#\203:^@\320\nB$
command-line()
normal-top-level()
```

It took a bit of time to figure out, but the problem cleared up once I removed all of the compiled versions of the elisp files (<code>*.elc</code>).

Here's the command to remove all files that end with the file extension <code>.elc</code> in the current directory and sub-directories:

```text
$ find . -name "*.elc" -type f | xargs rm -f
```

(seen <a href="https://gist.github.com/yuanmai/4411286">here</a>)
