---
title: Using ex to bulk-edit files
date: 2017-12-03
author: Josh
path: "/blog/using-ex-to-bulk-edit-files/"
---

I previously wrote about <a href="https://codeselfstudy.com/blogs/command-line-scripting-with-ed-and-ex">command line scripting with ed and ex</a>. I just had an opportunity to put ex into use in practice.

I needed to edit hundreds of files, searching for a line of text and then deleting it along with the next 22 lines.

I created an <code>exscript</code> file containing this code:

```
g/block_2/ .,+22 d
x
```

**Update:** you can probably simplify that deletion command to this:

```
g/block_2/d23
```

Then ran it on a file to test it:

```
$ ex - index.html < exscript
```

Once I confirmed that it worked correctly, I ran it on the entire directory:

```bash
for f in *.html
do
    ex - $f < exscript
done
```

This solution worked perfectly for my task, which was to remove a block of text from every page of a <a href="https://codeselfstudy.com/wiki/Wget">website downloaded with wget</a>.
