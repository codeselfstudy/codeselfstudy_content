---
title: Problems with Copying and Pasting Code in Vim?
date: 2017-04-03
author: Josh
path: "/blog/problems-with-copying-and-pasting-code-in-vim/"
---

I've written a tutorial on <a href="https://medium.com/@joshhostels/how-to-copy-paste-with-vim-registers-902d96e5c493">how to copy/paste from Vim registers</a>. I wanted to add a few more tips:

<h2>Problems with Pasting and Code Indentaion</h2>

If you're having trouble with indentation when pasting code into Vim (especially with indentation-sensitive languages like Python), there are a couple of possible solutions:

<h3>1. Paste using Vim registers</h3>

<div class="alert alert-info" role="alert">
  <strong>tl;dr</strong> From visual mode, use <code>"+y</code> to yank (copy) out of Vim when you're going to paste into some other application. Use <code>"+p</code> to paste from other applications into Vim.
</div>

Tip: read <a href="https://medium.com/@joshhostels/how-to-copy-paste-with-vim-registers-902d96e5c493">my other tutorial on Vim registers</a> or the vim help using <code>:help registers</code>.

There are ten types of registers in Vim. You can think of them like separate clipboards. Each clipboard has a name. The important one for copying/pasting between Vim and the system is the register called <code>+</code> (#8, below).

<blockquote>
<ol>
  <li>The unnamed register ""</li>
  <li>10 numbered registers "0 to "9</li>
  <li>The small delete register "-</li>
  <li>26 named registers "a to "z or "A to "Z</li>
  <li>three read-only registers ":, "., "%</li>
  <li>alternate buffer register "#</li>
  <li>the expression register "=</li>
  <li>The selection and drop registers "*, "+ and "~ </li>
  <li>The black hole register "_</li>
  <li>Last search pattern register "/</li>
</ol>
...

<pre><strong>8. Selection and drop registers "*, "+ and "~</strong>
Use these registers for storing and retrieving the selected text for the GUI.
See |quotestar| and |quoteplus|.  When the clipboard is not available or not
working, the unnamed register is used instead.  For Unix systems the clipboard
is only available when the |+xterm_clipboard| feature is present.  {not in Vi}

Note that there is only a distinction between "* and "+ for X11 systems.  For
an explanation of the difference, see |x11-selection|.  Under MS-Windows, use
of "* and "+ is actually synonymous and refers to the |gui-clipboard|.</pre>
</blockquote>

<h3>2. Use <code>:set paste</code></h3>

If you're using a Mac and trying to paste with command-v, the indentation might get distorted, depending on the contents of your <code>.vimrc</code> file.

You can fix that by typing <code>:set paste</code> before you paste and then doing <code>:set nopaste</code> when done. Those could be assigned to keybindings in your <code>.vimrc</code> file.

Here are the relevant docs on <code>paste</code>, which you can read by typing <code>:help paste</code> in Vim:

<blockquote><pre>
'paste'			boolean	(default off)
			global
			{not in Vi}
	Put Vim in Paste mode.  This is useful if you want to cut or copy
	some text from one window and paste it in Vim.  This will avoid
	unexpected effects.
	Setting this option is useful when using Vim in a terminal, where Vim
	cannot distinguish between typed text and pasted text.  In the GUI, Vim
	knows about pasting and will mostly do the right thing without 'paste'
	being set.  The same is true for a terminal where Vim handles the
	mouse clicks itself.
	This option is reset when starting the GUI.  Thus if you set it in
	your .vimrc it will work in a terminal, but not in the GUI.  Setting
	'paste' in the GUI has side effects: e.g., the Paste toolbar button
	will no longer work in Insert mode, because it uses a mapping.
	When the 'paste' option is switched on (also when it was already on):
		- mapping in Insert mode and Command-line mode is disabled
		- abbreviations are disabled
		- 'autoindent' is reset
		- 'expandtab' is reset
		- 'formatoptions' is used like it is empty
		- 'revins' is reset
		- 'ruler' is reset
		- 'showmatch' is reset
		- 'smartindent' is reset
		- 'smarttab' is reset
		- 'softtabstop' is set to 0
		- 'textwidth' is set to 0
		- 'wrapmargin' is set to 0
	These options keep their value, but their effect is disabled:
		- 'cindent'
		- 'indentexpr'
		- 'lisp'
	NOTE: When you start editing another file while the 'paste' option is
	on, settings from the modelines or autocommands may change the
	settings again, causing trouble when pasting text.  You might want to
	set the 'paste' option again.
	When the 'paste' option is reset the mentioned options are restored to
	the value before the moment 'paste' was switched from off to on.
	Resetting 'paste' before ever setting it does not have any effect.
	Since mapping doesn't work while 'paste' is active, you need to use
	the 'pastetoggle' option to toggle the 'paste' option with some key.</pre>
</blockquote>

<h2>Conclusion</h2>

I would use <code>"+p</code> and <code>"+y</code>, because once one understands registers, they can be used for many things. Learn more about them by opening up Vim and typing: <code>:help registers</code>.
