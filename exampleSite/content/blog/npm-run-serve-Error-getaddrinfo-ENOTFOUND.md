---
title: "SOLVED: Npm run serve Error: getaddrinfo ENOTFOUND"
description: "getaddrinfo ENOTFOUND, typically occurs when your Node.js project, is attempting to make a network request or establish a connection to a specific hostname, but it cannot resolve that hostname to an IP address. This failure in DNS resolution results in the error being thrown."
image: "images/post/post-13.png"
date: 2023-06-24T18:19:25+06:00
categories: ["programming"]
tags: ["programming", "vue.js", "node.js"]
type: "regular" # available types: [featured/regular]
draft: false
---

### `Error: getaddrinfo ENOTFOUND`
When trying to run a Vue CLI application, you might encounter an error message that reads `Error: getaddrinfo ENOTFOUND.`

This error typically occurs when Node.js tries to establish a connection to a specific hostname but fails to resolve that hostname to an IP address.

A simple fix to this is to manaually specify the host for the local server to run on.


{{< highlight bash >}}
  npm run serve -- --host=127.0.0.1
{{< /highlight >}}

<br> 

After running this command, the Vue CLI application will start running on the IP we specified.

{{< highlight bash >}}
 INFO  Starting development server...


 DONE  Compiled successfully in 20297ms                                                           22:21:19


  App running at:
  - Local:   http://127.0.0.1:8081/
  - Network: http://127.0.0.1:8081/

  Note that the development build is not optimized.
  To create a production build, run npm run build.
{{< /highlight >}}

#### Conclusion
If you encounter the getaddrinfo ENOTFOUND error while working with Vue CLI, try specifying the host manually using the --host flag. This should help you resolve the issue and get your application running smoothly.

Hope this was helpful to you



    