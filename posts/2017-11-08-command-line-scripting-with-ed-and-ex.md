---
title: Command line scripting with ed and ex
date: 2017-11-08
---

I just learned a little editing trick with <a href="https://en.wikipedia.org/wiki/Ed_(text_editor)">ed</a> and wanted to write some quick notes here.

Start with two files that are slightly different:

```
$ cat file1
the man o muse inform that many a way
wound with his wisdom to his wished stay
who wandered wonderous far when he the town
of sacred troy had sacked and shivered down
```

```
$ cat file2
The man, o muse inform, that many a way
wound with his wisdom to his wished stay
who wandered wonderous far when he the town
of sacred troy had sacked and shivered down
```

Diff them as an ed (or ex) script by using the `-e` flag:

```
$ diff -e file1 file2  > script1
```

Check the ed (or ex) script to see what it does (changes line 1 to the given line and finishes).

```
$ cat script1
1c
The man, o muse inform, that many a way
.
```

<del>The ed script will need to write back to the file, so add a "w" to the end of the ed script: `$ echo 'w' >> ed_script.diff`</del>

EDIT: there is <a href="http://www.linuxdevcenter.com/pub/a/linux/lpt/28_09.html">a better way</a> using `%p` -- for example:

```
cat script1; echo '%p' | ex - oldfile
```

Or even using multiple scripts:

```
cat script1 script2 script3; echo '%p' | ex - oldfile
```

Process the file with ed (or ex), using the saved script:

```
$ ed - file1 < script.diff
```

Now file1 has been updated to match file2:

```
$ cat file1
The man, o muse inform, that many a way
wound with his wisdom to his wished stay
who wandered wonderous far when he the town
of sacred troy had sacked and shivered down
```

I thought it was interesting, because it might be useful in other scripts.

<strong>Update:</strong> I found a use for it: <a href="https://codeselfstudy.com/blogs/using-ex-to-bulk-edit-files">Using ex to bulk-edit files</a>
