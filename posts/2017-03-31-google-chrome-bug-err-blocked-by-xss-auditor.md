---
title: Google Chrome Bug: ERR_BLOCKED_BY_XSS_AUDITOR
date: 2017-03-31
author: Josh
path: "/blog/google-chrome-bug-err_blocked_by_xss_auditor/"
---

This morning I was trying to write a quick blog post here, but when I submitted it, I got this error from Google Chrome:

<img src="/files/chrome-xss.png" width="720" height="447" alt="chrome-xss.png" />

<blockquote>This page isnt working

Chrome detected unusual code on this page and blocked it to protect your personal information (for example, passwords, phone numbers, and credit cards).
Try visiting the site's homepage.
ERR_BLOCKED_BY_XSS_AUDITOR</blockquote>

I know for sure that there was no personal information in the submitted content, because it was a list of MathJax tutorials along with a few code examples.

Not only did Chrome block me from posting the blog post, it deleted the history of my blog post from the browser so that I couldn't recover my text by using the back button.

Is anyone else encountering this problem? In the meantime, I will have to use <a href="https://www.firefox.com/">Firefox</a> to submit the blog post.

Update: it happened again with a different site when I tried to post embedded YouTube videos (which use iframe elements).

Update, April 30, 2017: I think this bug happens when previewing content that contains <code>iframe</code> or <code>script</code> tags. When both the source code and rendered tags are sent to the browser, Google Chrome blocks the submission. It should now be possible to reproduce the bug by posting a comment here on this site (using Google Chrome) and previewing the content before submitting it.
