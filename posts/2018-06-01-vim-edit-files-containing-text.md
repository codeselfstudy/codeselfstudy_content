title: How to Search Multiple Files for Text and Edit Them in Vim
date: 2018-06-01 11:24
category: Vim
slug: vim-search-edit-multiple-files
authors: Josh

Here's a quick one-liner for searching and editing files that contain specific text. This tutorial uses Vim, but it should work with any editor that accepts command line arguments.

For example, you might want to edit all the files in your project that contain the text 'hello world'.

-------

**2018-07-09 UPDATE:** a reader sent in the following tip, which works better than my examples below:

> Just do:
> `vi $(grep -lr 'Hello World')`
>
> Use git grep if you are in a git repo:
> `vi $(git grep -l 'Hello World')`

The `grep -l` option will list files that have matches.

-------

You can search for that text with the [grep command](https://en.wikipedia.org/wiki/Grep) like this:

```
$ grep -ri 'hello world' *
```

It should show a list of files that contain colons after the file names, something like this:

```text
$ grep -ri 'hello world' *
templates/base.html:Adipisicing incidunt hello world voluptates architecto molestias debitis Dignissimos nostrum facilis ex ex illo Incidunt non voluptatibus corporis alias officia Veritatis soluta ut quasi non nulla? Rerum ipsum architecto quod eveniet soluta?
templates/home.html:hello world
templates/home.html:hello world
```

You can then extract just the first column (the filenames) with the `cut` command:

```
$ grep -ri 'hello world' * | cut -d: -f1
```

That takes the output of `grep` and pipes it into `cut`. The `cut` command slices the columns using colon characters as the column delimiters (`-d:`) and extracts field 1 (`-f1`).

The result should be something like this:

```text
$ grep -ri 'hello world' * | cut -d: -f1
templates/base.html
templates/home.html
templates/home.html
```

You can then filter the list for unique results with the `uniq` command:

```
$ grep -ri 'hello world' * | cut -d: -f1 | uniq
```

The result should be something like this:

```text
$ grep -ri 'hello world' * | cut -d: -f1 | uniq
templates/base.html
templates/home.html
```

Wrap it in `$()` and make sure it produces the output you want:

```
$ echo $(grep -ri 'hello world' * | cut -d: -f1 | uniq)
```

Example output:

```text
$ echo $(grep -ri 'hello world' * | cut -d: -f1 | uniq)
templates/base.html templates/home.html
```

Notice that it's producing a list of filenames that could be passed into any program.

Pass the output of the command to vim:

```
vim $(grep -ri 'hello world' * | cut -d: -f1 | uniq)
```

Or if you want to open them in Vim tabs, use the `-p` option:

```
vim -p $(grep -ri 'hello world' * | cut -d: -f1 | uniq)
```

If you want to learn more about how each command works, use the `man` command to view the documentation:

```text
$ man grep
$ man cut
$ man uniq
```
