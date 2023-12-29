---
title: "Resolving Makefile Errors: make: *** No rule to make target 'start'.  Stop."
description: "GNU make versions below 3.78 didn't handle Windows CRLF newlines properly
If you have a lower version u might want to update that by simply going to the [site][http://gnuwin32.sourceforge.net/packages/make.html] and downlaoding it."
image: "images/post/post-11.png"
date: 2023-10-12T18:19:25+06:00
categories: ["programming"]
tags: ["makefile"]
type: "reguler" # available types: [featured/regular]
draft: false
sitemapExclude: false
---

I was getting ths error and when I tried to start my makefile on windows desktop, fortunately I found a way to resolve the issue. I hope this guide should help you troubleshoot and resolve issues you may face while working with Makefiles on a Windows desktop.

### Checking Your Make Version
The first step you need to take is to verify the version of GNU make installed on your system. Run 
`make --version` in your terminal to check this. 

Versions below 3.78 of GNU make have known issues handling Windows CRLF newlines correctly.

If you're running a version older than 3.78, consider updating it. You can download the latest version from the [GNU Win32 project page][http://gnuwin32.sourceforge.net/packages/make.html].


#### Correct Spelling of Makefile
If you're running a version above 3.78, another common issue could be the incorrect spelling of your Makefile. Ensure that it's spelled as `Makefile`, with a lowercase `'f'`. Using `MakeFile` or any other variation will lead to errors.

#### Handling Missing Separator Errors
After ensuring that your Makefile is named correctly, you might encounter a missing separator error. This error typically looks like this: `Makefile:7: *** missing separator. Stop.`

This error occurs when you use spaces instead of tabs for indentation in your Makefile. Make is very particular about this - it expects tabs, not spaces. Here's an example of correct indentation:

{{< highlight bash >}}
run: build
	@echo Starting back end...
	set DSN=${DSN}&& start /B .\${BINARY_NAME} &
	@echo back end started!
{{< / highlight >}}

In the above example, note that there's a tab character before `@echo`, not four spaces. If you're using Visual Studio Code, you can easily convert spaces to tabs by opening the command palette, using `settings/command pallete` or `(Ctrl + Shift + P)`, search for `"Indentation"`, and select `"Convert Indentation to Tabs"`. 

After doing this, clear all the spaces in your Makefile and insert tabs instead.
And that's it.
That's how I solved my problem, hope this helps you.

