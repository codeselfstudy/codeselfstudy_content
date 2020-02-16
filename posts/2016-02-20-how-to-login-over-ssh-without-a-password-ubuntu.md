---
title: How to Login over SSH without a Password (Ubuntu)
date: 2016-02-20
path: "/blog/how-to-login-over-ssh-without-a-password-ubuntu/"
---

This page has instructions on how to get started with passwordless login to remote servers over SSH.

You will need to generate a pair of keys on your local machine and then copy the public key to the remote machine.

Look for instructions that are specific to whatever server that you're using. E.g., <a href="https://help.github.com/articles/generating-an-ssh-key/">Github</a>, <a rel="nofollow" href="https://kb.site5.com/shell-access-ssh/how-to-generate-ssh-keys-and-login-to-your-account-with-ssh/">Site5</a>.

Basically, you want to check if there are existing keys:

```text
$ ls -al ~/.ssh
```

If you don't have keys there, you will need to <a href="https://help.github.com/articles/generating-a-new-ssh-key/">generate some</a>.

A problem that I was running into was that Ubuntu would keep prompting me to enter my key passphrase every time, which defeated one of the reasons for passwordless login.

The messages looked like:

```text
Enter passphrase for key '/home/username/.ssh/id_dsa':
```

To get rid of the password prompt on each login, type <code>ssh-add</code> and enter your passwords for the last time.
