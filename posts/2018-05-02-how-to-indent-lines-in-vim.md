---
title: How to Reindent Lines in Vim
date: 2018-05-02 14:45
category: Vim
author: Josh
path: "/blog/reindent-lines-in-vim/"
---

Reindenting files helps keep code neat. In Vim, you can reindent an entire file from normal mode (press `ESC` to get there) by typing `gg=G`.

You can reindent multiple files with the following commands, in this case reindenting all JavaScript files in the current directory:

```text
:ar *.js
:argdo norm gg=G
:wall
```

You can find more information about those commands with `:h` like this:

```text
:h ar
```

See [the Vim wiki](http://vim.wikia.com/wiki/Shifting_blocks_visually) for more ideas.
