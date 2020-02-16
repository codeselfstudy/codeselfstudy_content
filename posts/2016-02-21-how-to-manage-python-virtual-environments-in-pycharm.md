---
title: How to Manage Python Virtual Environments in PyCharm
date: 2016-02-21
author: Josh
path: "/blog/how-to-manage-python-virtual-environments-in-pycharm/"
---

Creating virtual environments on Windows can be challenging. (There is <a href="http://codeselfstudy.com/blogs/python-virtualenv-and-virtualenvwrapper-tutorial-for-ubuntu-1404">an easier way on Linux and Mac</a>.) When on Windows, PyCharm can help you set up and manage your virtual environments.

If you don't already have it, get the free <a href="https://www.jetbrains.com/pycharm/">community edition version of PyCharm</a>.

To create a new virtualenv, go to File -> Settings, and search for project interpreter like in the screenshot below.

<img src="/files/pycharm-project-interpreter.png" width="652" height="376" alt="pycharm-project-interpreter.png" />

Look for the gear icon on the top right:

<img src="/files/pycharm-virtualenv.png" width="367" height="223" alt="PyCharm virtualenv" />

Click the gear, and choose what you want to do:

<img src="/files/pycharm-choose-virtual-env.png" width="203" height="190" alt="pycharm-choose-virtual-env.png" />

When you create a new virtualenv,  it will look something like the screenshot below.

<img src="/files/make-virtualenv.png" width="373" height="245" alt="mkvirtualenv" />

The next thing to do is install any required packages. Look for the plus sign on the right:

<img src="/files/pycharm-virtualenv-install-package.png" width="367" height="223" alt="pycharm-virtualenv-install-package.png" />

You can then search for the needed package and install it:

<img src="/files/pycharm-install-package.png" width="486" height="405" alt="pycharm-install-package.png" />

More information <a href="https://www.jetbrains.com/pycharm/help/creating-virtual-environment.html">here</a>.

If you have any questions, leave a comment below.
