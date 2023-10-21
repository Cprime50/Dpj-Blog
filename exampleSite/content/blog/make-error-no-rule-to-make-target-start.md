---
title: "How To Fix: make: *** No rule to make target 'start'.  Stop."
description: "GNU make versions below 3.78 didn't handle Windows CRLF newlines properly
If you have a lower version u might want to update that by simply going to the [site][http://gnuwin32.sourceforge.net/packages/make.html] and downlaoding it."
image: "images/post/golang-bufio-with-float-input.png"
date: 2023-03-12T18:19:25+06:00
categories: ["programming"]
tags: ["makefile", "coding", "golang"]
type: "featured" # available types: [featured/regular]
draft: false
sitemapExclude: false
---

I was getting ths error and when I tried to start my makefile on windows desktop, fortunately I found a way to resolve the issue.

### Firstly
run make --version to check what version of make you have installed on your computer
GNU make versions below 3.78 didn't handle Windows CRLF newlines properly

If you have a lower version u might want to update that by simply going to the [site][http://gnuwin32.sourceforge.net/packages/make.html] and downlaoding it.


If you have a version above 3.78 then make sure that your `Makefile` is spelled corrctly, not `MakeFile` but spelled as `Makefile`, `f` in lowercase.

### Secondly
If the steps above have worked for you. You'll be getting a new type of error,but dont worry this is great because it means that 
make can now find your `Makefile`
the error  will look as follows:
    `Makefile:7: *** missing separator.  Stop.`
This is an  easy fix. All its telling you is that you need to have tabs and not four spaces for every command you want to run
Dont know why make its really picky about that

exaample:
{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
run: build
	@echo Starting back end...
	set DSN=${DSN}&& start /B .\${BINARY_NAME} &
	@echo back end started!
{{< / highlight >}}

You shouldnt have 4 spaces before @echo, instead a tab otherwise you will get an error.
On vscode you can fix the indentation issue by going to `settings/command pallete` or `(ctrl + shift + p)`
Search indentation and select convert indentation to tabs. Then go back to your `Makefile`, clear all the spaces and insert tabs.
And that's it.

