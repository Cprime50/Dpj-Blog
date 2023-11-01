---
title: "Resolving a Hugo Error: resources in Concat must be of same media type, got text/x-scss and text/css "
description: "If you're using Hugo to build your websites, you may have encountered errors during the build process. These errors can sometimes be cryptic, leaving you scratching your head, wondering how to fix them. In this blog post, we'll explore a common Hugo error related to Bootstrap SCSS module and share how we successfully resolved it."
image: "images/post/post-11.png"
date: 2023-03-12T18:19:25+06:00
categories: ["programming"]
tags: ["bufio", "coding", "golang"]
type: "reguler" # available types: [featured/regular]
draft: false
sitemapExclude: false
---



#### Resolving a Hugo Error

If you're using Hugo to build your websites, you may have encountered errors during the build process. These errors can sometimes be cryptic, leaving you in a state of fustration, wondering how to fix them. In this blog post, we'll explore a common Hugo error related to Bootstrap SCSS module and share how we successfully resolved it.


## The Error Message

The error message we encountered looked like this:

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
Error: Error building site: TOCSS: failed to transform "main_parsed.scss" (text/x-scss): resource "scss/scss/main.scss_6c95cc1249b26b124274204dbf970c34" not found in file cache

"/modules/filecache/modules/pkg/mod/github.com/twbs/bootstrap@v5.3.0+incompatible/scss/_maps.scss:55:16
{{< /highlight >}}

At first glance, it might seem like a daunting issue to tackle, especially if you're not well-versed in Hugo's inner workings or SCSS. However, with some troubleshooting and a bit of patience, we were able to identify and fix the problem.

## Understanding the Error

The error message essentially tells us that there is an issue with our boostrap version compatability.

## Troubleshooting Steps

To resolve this error, we took the following steps:

### 1. Checking Bootstrap Version

We realized that the error occurred after a recent Hugo update. This led us to suspect that the Bootstrap module we were using might not be compatible with the latest Hugo version. To confirm this, we checked the Bootstrap module's version.

### 2. Downgrading the Bootstrap Module

To fix the error, we decided to downgrade the Bootstrap module to a version that we knew was compatible with our Hugo setup. We used the following command to downgrade the module:

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
go get github.com/gohugoio/hugo-mod-bootstrap-scss/v5@v5.20200.20101
{{< /highlight >}}

This command fetches the specific version of the Bootstrap module that we wanted.

### 4. Clearing Hugo's Cache

We also cleared Hugo's cache to ensure that any cached files or outdated dependencies wouldn't interfere with our build process. To do this, we deleted the contents of the "hugo_cache" folder in our project directory.

### 5. Rebuilding the Project

After downgrading the Bootstrap module and clearing Hugo's cache, we rebuilt our Hugo project. To our relief, the error was gone, and our project compiled successfully.

## Conclusion

Encountering errors during web development projects is a common occurrence, and it's essential not to get discouraged. Instead, view these errors as opportunities to learn and improve your skills. In our case, we successfully resolved the "Undefined variable" error by downgrading the Bootstrap module and ensuring compatibility with our Hugo version.

Remember that troubleshooting and problem-solving are valuable skills in web development. If you encounter similar issues in your Hugo projects, don't hesitate to explore different solutions, seek help from the community, and document your findings. Happy coding!