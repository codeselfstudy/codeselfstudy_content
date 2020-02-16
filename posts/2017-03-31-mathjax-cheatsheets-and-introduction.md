---
title: MathJax Cheatsheets and Introduction
date: 2017-03-31
---

<a href="https://www.mathjax.org/">MathJax</a> is a JavaScript library that allows people to embed mathematical formulas in web pages using various formats like TeX, MathML, and ASCIImath. MathJax is installed on this website, so anyone can use it in the forum, blogs, and wiki.

<strong>Sample output:</strong> MathJax allows users to enter TeX and get back formulas like this:

$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$

<h2>How to Install MathJax</h2>

You can install MathJax by including a `<script>` tag from a CDN <a href="https://cdnjs.com/libraries/mathjax">like cdnjs</a>. For example, you could copy/paste this script tag into your site, just before the closing `</body>` tag:

```html
<script src="//cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" integrity="sha256-yYfngbEKv4RENfGDvNUqJTqGFcKf31NJEe9OTnnMH3Y=" crossorigin="anonymous"></script>
```

If MathJax appears to be loading, but doesn't render the math symbols, be sure that the MathJax URL has these parameters on the end: <code>?config=TeX-AMS-MML_HTMLorMML</code>

MathJax can also be installed with NPM or downloaded to your server.

<h2>The MathJax Cheatsheets</h2>

I often need to look up Mathjax symbols. These are the most useful references I've found:

<ul>
  <li><a href="https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-qu%E2%80%8C%E2%80%8Bick-reference">MathJax Tutorial</a></li>
  <li><a href="http://www.onemathematicalcat.org/MathJaxDocumentation/TeXSyntax.htm">TeX Syntax</a></li>
</ul>

<h2>Quickstart</h2>

To embed MathJax into a site, surround the markup with backslash-escaped parentheses, like this:

```
\( \cfrac{2}{1+\cfrac{2}{1+\cfrac{2}{1}}} \)
```

Example output: \\( \cfrac{2}{1+\cfrac{2}{1+\cfrac{2}{1}}} \\)

To display the output as a block, use backslash-escaped square brackets:

```
\[ \cfrac{2}{1+\cfrac{2}{1+\cfrac{2}{1}}} \]
```

Example output:

\\[ \cfrac{2}{1+\cfrac{2}{1+\cfrac{2}{1}}} \\]

MathJax will work anywhere on this site: the <a href="/forum">forum</a>, <a href="http://codeselfstudy.com/wiki/Main_Page">wiki</a>, and <a href="/blog">blogs</a>.
