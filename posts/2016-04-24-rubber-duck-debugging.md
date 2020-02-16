---
title: Rubber Duck Debugging
date: 2016-04-24
path: "/blog/rubber-duck-debugging/"
---

Have you ever asked someone a debugging question and then realized the answer yourself while you were walking through the explanation of the error? There is a debugging technique called <a href="https://en.wikipedia.org/wiki/Rubber_duck_debugging">rubber duck debugging</a> that works in similar way.

It requires a rubber duck (or similar assistant). You can explain your error message to the duck, walking it through all of the steps, including the stack trace. During the process of explaining the problem in detail, you are likely to solve the problem yourself.

Basically the order of investigation should be something like:

<ol>
    <li>Google the error message.</li>
    <li>Remove the project-specific parts of the error message and Google it again. For example, if your error message contains your username and folder names in the paths that are printed to the screen, remove those user-specific parts of the error message before pasting it into Google.</li>
    <li>Paste increasingly smaller parts of the error message into Google to see if an answer comes up. Try to think about what words someone would use in a Stack Overflow question if they were trying to solve their problem.</li>
    <li>Search Stack Overflow.</li>
    <li><strong>Try talking to the rubber duck.</strong></li>
    <li>Ask a friend or coworker, if one is nearby. (Don't do this without Googling the error message and talking to the rubber duck first, because it's likely that they are going to have to perform those steps for you.)</li>
    <li>Post the question on a <a href="https://community.codeselfstudy.com/">programming forum</a>, Stack Overflow, or in a chatroom, like IRC</li>
</ol>

If you don't want to carry around a rubber duck, you could use an animal sticker or even a dinosaur for a reminder.

<img src="/files/diana-sor.jpg" width="600" height="406" alt="Rubber duck debugging" /><br>
<small>A portable debugging tool</small>
