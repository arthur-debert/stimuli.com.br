---
layout: post
title: "Hello VIM, or quitting TextMate cold turkey"
permalink: "/trane/2009/sep/21/hello-vim-or-quitting-textmate-cold-turkey/"
tags: [vim textmate editors]
categories: [trane]
legacy_id: 30
date: "2009-09-21 -0300"
---
In my [last post](http://www.stimuli.com.br/trane/2009/sep/19/how-i-learn-stop-worrying-and-love-vim/) I've mentioned my way through VIM. Quiting TextMate cold turkey wasn't easy. But fear not: there are a bunch of plugins that will make it a breeze. Bellow a list of the best ones to fill the gap:

- [DelimitMate](http://www.vim.org/scripts/script.php?script_id=2754) When in insert mode, will auto balance paired delimiters (parenthesis, brackets, quotes, angle brackets). This is a default in TextMate, when you type a balanced delimiter it inserts the closing one and puts the cursor in the middle. This is a pretty new plugin, I don't think it has received the attention it deserves.  
- [NerdTree](http://www.vim.org/scripts/script.php?script_id=1658) A file explorer thing, similar to the project drawer in TextMate.
- [NerdCommenter](http://www.vim.org/scripts/script.php?script_id=1218): A plugin that makes commenting source code dead easy. Supports many languages, and has smart settings (toggle, visual mode, etc).
- [Fuzzy Finder TextMate](http://github.com/jamis/fuzzyfinder_textmate). This was the feature that I missed the most: a quick way to navigate through files (aka command T) also through tags in a source file (aka command shift T). Just brilliant, and also adds some nifty features such searching from the most recently used files. This plugin required ruby support. 
- [SnipMate](http://www.vim.org/scripts/script.php?script_id=2540): snippets support, much like TextMate's. 
- [YankRing](http://www.vim.org/scripts/script.php?script_id=1234) implements a kill ring for the yank buffer. Pretty much like TextMate's copy and paste history, but more configurable and powerful: VIM style.

With those plugins in place, there aren't any major features missing. Having those plugins for VIM is a testimony of how TextMate has really brought good ideas into the editor scene. It also corroborates VIM's extensibility. Even under primitive constrains (no GUI, terminal only), VIM is able to mimic those features.

Also, other plugins that I've found essential:

- [Surround](http://www.vim.org/scripts/script.php?script_id=1697): smartly inserts, changes and removes balanced delimiters including XML tags. 
- [Taglist](http://www.vim.org/scripts/script.php?script_id=273): parses and helps you to navigate through structured source code.
- [Align](http://www.vim.org/scripts/script.php?script_id=294): makes source code alignment a breeze (hard to explain, give it a shot).

All in all, with the right plugins, VIM can match most of TextMate's features. Are there any other plugins I should know about?