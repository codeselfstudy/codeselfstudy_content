---
title: How to solve the "WARNING! Your environment specifies an invalid locale" Error
date: 2017-04-09
path: "/blog/how-to-solve-the-warning-your-environment-specifies-an-invalid-locale-error/"
---

On logging into a remote server, I got an error that began with: <code>WARNING! Your environment specifies an invalid locale.</code>. This is how I fixed it:

I entered each one of these commands in the terminal. The last one reboots the server.

```bash
locale
export LANGUAGE=en_US.UTF-8; export LANG=en_US.UTF-8; export LC_ALL=en_US.UTF-8; locale-gen en_US.UTF-8
sudo dpkg-reconfigure locales
sudo shutdown -r 0
```

Read more <a href="https://www.digitalocean.com/community/questions/warning-your-environment-specifies-an-invalid-locale-this-can-affect-your-user-experience-significantly-including-the-ability-to-manage-packages">here</a>.
