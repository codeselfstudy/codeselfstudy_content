---
title: How to Send Desktop Notifications in Linux
date: 2018-05-11 20:31
category: GNU/Linux
tags: Ubuntu
authors: Josh
path: "/blog/send-desktop-notifications-linux/"
---

This post explains how to send custom desktop notifications in GNU/Linux. These commands were tested on Ubuntu 16.04.

The command to use is `notify-send` followed by a title and optional body.

```bash
notify-send 'The Title' 'The Body'
```

It looks something like this on my computer:

![notify-send output on Ubuntu 16.04](/images/2018-05/notify-send-gnu-linux.png)

The command can accept options too.

## Options

### Icons

You can show an icon in the notification. On Ubuntu 16.04, the icons [come from](https://askubuntu.com/a/189262) `/usr/share/icons/gnome/32x32`.

Try these examples to see how it works:

```bash
notify-send -i filesaveas 'File saved' 'kitten.gif was saved to ~/Downloads'
notify-send -i call-start 'Incoming Call' 'Alice is calling'
# note the backticks below which output the current date
notify-send -i weather-few-clouds 'Weather Report' "It's partly cloudy on `date`"
```

You can use custom icons like this:

```bash
notify-send -i ~/Pictures/kitten.jpg 'Incoming Kitten' 'meow'
```

It looks like this:

![Kitten pic](/images/2018-05/kitten-pic.png)

The source image in that screenshot was 100x100 pixels.

### Urgency

The order of the notifications can be set with the `-u` (`--urgency`) option.

Here are some examples:

```bash
notify-send -u 'normal' 'Message' '1: normal urgency message'
notify-send -u 'low' 'Message' '2: low urgency message'
notify-send -u 'critical' 'Message' '3: critical urgency message'
```

If you paste all three lines into a terminal at once, message #3 will show before message #2 because of the `critical` urgency.

### Expire Time

The man page says that "Ubuntu's Notify OSD and GNOME Shell both ignore this parameter", but the `-t` option should otherwise set the notification time in milliseconds.

### More Options

You can type `man notify-send` for a couple more options.
