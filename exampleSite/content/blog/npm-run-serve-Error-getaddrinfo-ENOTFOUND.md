---
title: "How to fix Npm run serve Error: getaddrinfo ENOTFOUND"
description: "getaddrinfo ENOTFOUND, typically occurs when your Node.js project, is attempting to make a network request or establish a connection to a specific hostname, but it cannot resolve that hostname to an IP address. This failure in DNS resolution results in the error being thrown."
image: "images/post/post-13.png"
date: 2023-08-24T18:19:25+06:00
categories: ["programming"]
tags: ["programming", "vue.js", "node.js"]
type: "regular" # available types: [featured/regular]
draft: false
---

### `Error: getaddrinfo ENOTFOUND`
I was trying to set up my vue-cli app to run at local host but kept getting the error below.

Note: I ran the following command:
{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
    npm run serve
{{< /highlight >}}

<br> 


{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
    vue serve
{{< /highlight >}}

<br> 

They both gave me the same error which looked something like this:

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
            throw error;
        ^

Error: getaddrinfo ENOTFOUND 75faeb277b4853
    at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:107:26) {
  errno: -3008,
  code: 'ENOTFOUND',
  syscall: 'getaddrinfo',
  hostname: '75faeb277b4853'
}

Node.js v18.15.0

    {{< /highlight >}}

<br> 

My suspicion was that node is trying to establish a connection to a specific hostname, but it cannot resolve that hostname to an IP address, which causes it to fail.


`A`fter trying out a couple of ways and alot of googling to no avail. I figured I could just manually specify the host it should run on maybe that could work.
Thanks to a [blog article](https://dev.to/clericcoder/how-to-start-a-development-server-for-your-project-2h5o) I found, I was able to understand how to do this. Simply by using the --host flag I was able to specify a host for my local server to run on.

<br>

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=22"  >}}
  npm run serve -- --host=127.0.0.1
{{< /highlight >}}

<br>

Phewwww, this worked. Instead of the `getaddinfo error` I kept getting. I finally got a successful response from the cli:

{{< highlight bash >}}
 INFO  Starting development server...


 DONE  Compiled successfully in 20297ms                                                           22:21:19


  App running at:
  - Local:   http://127.0.0.1:8081/
  - Network: http://127.0.0.1:8081/

  Note that the development build is not optimized.
  To create a production build, run npm run build.
{{< /highlight >}}

<br>

Our app is now successfully up and running locally.. Hopefully this helps you.


#### Lastly
The reason it runs on port :8081 for me could probably be that I already have something running on port :8080 , `an annoying EDB postgres instance`, I tried shutting that down on windows but it just refuses to go off. Well that's it, thanks for reading.




    