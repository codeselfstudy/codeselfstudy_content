---
title: How to Slugify Strings in Bash
html_title: How to Slugify Strings in Bash for Static Site Generators
date: 2018-05-05 21:16
category: Shell Scripting
tags: Bash, Static Site Generators
author: Josh
path: "/blog/how-to-slugify-strings-in-bash/"
---

In order to create new posts in static site generators, I'm using a Makefile command to create slugified filenames.

With this command in a Makefile, you can type something like `make newpost title='the title of the post'`, and a file with the correct filename will be created and opened in Vim.

I'll explain it in detail below, but here's a quick example that works in a terminal:

```text
$ echo content/blog/$(date +%Y-%m-%d)-$(echo -n 'hello world' | sed -e 's/[^[:alnum:]]/-/g' | tr -s '-' | tr A-Z a-z.md).md
```

and the output:

```text
content/blog/2018-05-05-hello-world.md
```

Here's the full command, extracted from the Makefile:

```
BASEDIR=$(CURDIR)

newpost:
	vim +':r templates/post.md' $(BASEDIR)/content/blog/$$(date +%Y-%m-%d)-$$(echo -n $${title} | sed -e 's/[^[:alnum:]]/-/g' | tr -s '-' | tr A-Z a-z.md).md
```

I'm sure that there are nicer ways to do this than with shell commands, but sometimes it's fun to tinker.

## Walkthrough

I'll use the string `'Saλuton Mondo! @123'` as an example, because it contains mixed case and some symbols and unicode.

### Opening Vim and Sending in Commands

You can pass commands into Vim during launch with the syntax below. This example opens Vim and reads in the contents of `templates/post.md` which is a basic template for a new blog post. `<filename>` will be a generated string:

```text
$ vim +':r templates/post.md' <filename>
```

### Slugifying the Filename

[Sed](https://www.gnu.org/software/sed/manual/sed.html) is a stream editor that is useful for quick text substition on the command line.

You can pipe strings into Sed like this:

```text
$ echo 'Saλuton Mondo @123' | sed -e 's/[^[:alnum:]]/-/g'
```

The `'s/foo/bar/g'` syntax is just a search and replace using a regular expression.

That example takes the string and replaces anything that is not alphanumerica with a dash. Running it produces this result, which is not exactly what is wanted:

```text
Saλuton-Mondo--123
```

Duplicate dashes can be removed with the translate (`tr`) command using the `-s` (squeeze repeats) option:

```text
$ echo 'Saλuton Mondo @123' | sed -e 's/[^[:alnum:]]/-/g' | tr -s '-'
```

The output is now:

```text
Saλuton-Mondo-123
```

The `tr` command can also be used to downcase characters like this:

```text
$ echo 'Saλuton Mondo @123' | sed -e 's/[^[:alnum:]]/-/g' | tr -s '-' | tr A-Z a-z
```

producing:

```text
saλuton-mondo-123
```

It can then be wrapped in `$()` with `.md` on the end for a file extension:

```text
$ echo $(echo 'Saλuton Mondo @123' | sed -e 's/[^[:alnum:]]/-/g' | tr -s '-' | tr A-Z a-z).md
```

to get:

```text
saλuton-mondo-123.md
```

Once again, in the Makefile, it looks like this, with double `$$` to escape the variables that aren't defined in the Makefile:

```
BASEDIR=$(CURDIR)

newpost:
	vim +':r templates/post.md' $(BASEDIR)/content/blog/$$(date +%Y-%m-%d)-$$(echo -n $${title} | sed -e 's/[^[:alnum:]]/-/g' | tr -s '-' | tr A-Z a-z.md).md
```

I hope that someone can find it useful for quickly starting new blog posts in static site generators. If you have additional ideas for improvements, leave a comment below.
