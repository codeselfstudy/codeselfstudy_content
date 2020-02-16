---
title: How to Compress and Extract tar.bz2 Files in the Terminal
date: 2017-04-08
author: Josh
path: "/blog/how-to-compress-and-extract-tarbz2-files-in-the-terminal/"
---

Quick tip: to create a backup of a directory (like a website) with a <code>.tar.bz2</code> format, you can compress it like this:

<ol>
  <li>To compress a directory, you can use: <code>tar -cjvf BACKUP_my_directory.tar.bz2 ./www</code></li>
  <li>To extract the tar.bz2 file do: <code>tar -xjf BACKUP_my_directory.tar.bz2</code></li>
</ol>
