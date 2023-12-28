---
title: "Github actions: Action failed with "The process '/usr/bin/git' failed with exit code 128"
description: "If youre getting this error while trying to use gitub actions you need to give actions read write permision in that repo."
image: "post-4.png"
date: 2023-11-26 T18:19:25+06:00
categories: ["programming"]
tags: ["github"]
type: "regular" # available types: [featured/regular]
draft: false
---

Actions permission

Action failed with "The process '/usr/bin/git' failed with exit code 128"

If youre getting this error while trying to use gitub actions you need to give actions read write permision in that repo.

Go to settings, actions, general,

Select any action or reuable workflow can be used
Actions permissions


Any action or reusable workflow can be used, regardless of who authored it or where it is defined.

The Actions tab is hidden and no workflows can run.

Any action or reusable workflow defined in a repository within Cprime50 can be used.

Any action or reusable workflow that matches the specified criteria, plus those defined in a repository within Cprime50, can be used. Learn more about allowing specific actions and reusable workflows to run.

Save 

then:

 scroll down to work flow permissions 
Workflow permissions
and give read and write permission 


Choose the default permissions granted to the GITHUB_TOKEN when running workflows in this repository. You can specify more granular permissions in the workflow using YAML. Learn more about managing permissions.



Workflows have read and write permissions in the repository for all scopes.

Workflows have read permissions in the repository for the contents and packages scopes only.