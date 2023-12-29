---
title: "Github actions: Action failed with "The process '/usr/bin/git' failed with exit code 128"
description: "The error message The process '/usr/bin/git' failed with exit code 128 typically indicates that GitHub Actions does not have the required permissions to execute certain tasks in your repository. This could be due to restrictions on the actions that can be run, or limitations on the scope of the workflows."
image: "images/post/post-4.png"
date: 2023-11-26 T18:19:25+06:00
categories: ["programming"]
tags: ["github"]
type: "regular" # available types: [featured/regular]
draft: false
---



### Troubleshooting GitHub Actions Permissions: A Comprehensive Guide

GitHub Actions is a powerful tool that allows developers to automate their software development workflows. However, sometimes, you might encounter errors while using it. One such error is `The process '/usr/bin/git' failed with exit code 128`, which is often due to insufficient permissions. This article will guide you through the steps to grant the necessary permissions to resolve this issue.

#### Granting Necessary Permissions
To resolve this issue, you need to adjust the permissions in your repository's settings. Here are the steps to do so:

1. Navigate to your repository's Settings: From your GitHub repository page, click on the 'Settings' tab located at the top right corner of the page.

2. Select Actions under the General category: In the left sidebar of the Settings page, you will find a section labeled 'General'. Click on 'Actions' within this section.

3. Choose Any action or reusable workflow can be used: In the Actions permissions section, select the option 'Any action or reusable workflow can be used'. This setting allows actions from any source to be used in your repository, providing flexibility in your workflows.


4. Set Workflow permissions: Scroll down to the 'Workflow permissions' section. Set the permissions to 'Workflows have read and write permissions in the repository for all scopes'. This setting grants comprehensive permissions to your workflows, enabling them to perform read and write operations in your repository.

5. Save your changes: After making these changes, remember to save them. Your settings should now allow GitHub Actions to perform the necessary operations without encountering the exit code 128 error.

By configuring these permissions, you provide GitHub Actions with the necessary access to perform read and write operations in your repository. This should resolve the exit code 128 error.

Feel free to adjust the settings based on your specific needs and security considerations. 