---
title: How to Delete Blank Lines in Vim
date: 2017-11-16
---

To delete all blank lines in a file using Vim (or nvim), you can do this:

```
:g/^\s*$/d
```

Read more <a href="http://vim.wikia.com/wiki/Remove_unwanted_empty_lines">here</a>.
