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



#### Overcoming Hugo Errors: A Step-by-Step Guide

Building websites with Hugo can sometimes present unexpected challenges, particularly when encountering errors during the build process. These errors can often feel cryptic and frustrating, leaving you unsure of how to proceed. In this article, we delve into a common Hugo error related to the Bootstrap SCSS module and provide a detailed walkthrough of how we successfully resolved it.


## The Error Message

The error message we encountered  was as follows:

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
Error: Error building site: TOCSS: failed to transform "main_parsed.scss" (text/x-scss): resource "scss/scss/main.scss_6c95cc1249b26b124274204dbf970c34" not found in file cache

"/modules/filecache/modules/pkg/mod/github.com/twbs/bootstrap@v5.3.0+incompatible/scss/_maps.scss:55:16
{{< /highlight >}}


## Understanding the Error

The error message essentially indicates a compatibility issue between our current Bootstrap version and the Hugo version we're using.

## Troubleshooting Steps

To resolve this error, we took the following steps:

### 1. Verifying the Bootstrap Version

We noticed that the error surfaced after a recent Hugo update. This led us to suspect that the Bootstrap module we were using might not be compatible with the latest Hugo version. To confirm this suspicion, we checked the version of the Bootstrap module.

### 2. Downgrading the Bootstrap Module

To rectify the error, we decided to downgrade the Bootstrap module to a version that we knew was compatible with our Hugo setup. We executed the following command to downgrade the module:

{{< highlight bash >}}
go get github.com/gohugoio/hugo-mod-bootstrap-scss/v5@v5.20200.20101
{{< /highlight >}}

This command fetches the specific version of the Bootstrap module that we needed.

### 4. Clearing Hugo's Cache

We also cleared Hugo's cache to ensure that any cached files or outdated dependencies wouldn't interfere with our build process. To do this, we deleted the contents of the "hugo_cache" folder in our project directory.

### 5. Rebuilding the Project

After downgrading the Bootstrap module and clearing Hugo's cache, we rebuilt our Hugo project. To our relief, the error was gone, and our project compiled successfully.



