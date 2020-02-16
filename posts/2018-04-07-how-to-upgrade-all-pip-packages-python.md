---
title: How to Upgrade All Pip Packages (Python)
date: 2018-04-07
---

Here's a quick and easy way to upgrade all outdated pip/Python packages on a computer. It worked for me on Ubuntu 16.04, and looks like it will work on Mac and Windows too.

Save a list of Python packages to a file:

```
$ pip freeze > pip_frozen.txt
```

Then run this command (which might require `sudo` on some systems) -- it will upgrade every Python package listed in that file:

```
$ pip install -r pip_frozen.txt --upgrade
```

Seen <a href="https://stackoverflow.com/a/33667992/1365699">here</a>.
