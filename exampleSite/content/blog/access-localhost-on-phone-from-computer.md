---
title: "Access localhost from mobile phone when connected to computer wifi"
description: "The first step is to find the IP address of your computer. This is a unique identifier for your device on the network. On Windows, open Command Prompt and type:
"
image: "images/post/post-13.png"
date: 2023-9-25 T18:19:25+06:00
categories: ["programming"]
tags: ["localhost", "ubuntu"]
type: "reguler" # available types: [featured/regular]
draft: false
---

Being able to test your website or application on your phone while developing it on your desktop seems like a very interesting idea, right?. 

Or perhaps you're working remotely and need to access files on your home computer. 
With the right setup, you can do all of these things and more. But how does it work? We'll go through that in this article.

Let's get started...

#### Prerequisites
Before we start, ensure that both your phone and computer are connected to the same WiFi network. If your computer doesn't have a WiFi adapter, you can use your phone's mobile hotspot to create a temporary WiFi network and connect to it on your desktop.

#### Finding Your PC's IP Address
The first step is to find the IP address of your computer. This is a unique identifier for your device on the network. On Windows, open Command Prompt and type:

{{< highlight bash >}}
ipconfig /all
{{< /highlight >}}

On MacOS or Linux, open Terminal and type:

{{< highlight bash >}}
ifconfig -a
{{< /highlight >}}

The IP address should start with `192` and not be a regular local IP like `127 or 172`. It should look something like this: `192.168.x.x.` .

#### Updating Your Server Settings
Next, you need to update your server settings to accept connections from any IP address. By default, your server may be set to only accept connections from the local host (127.0.0.1), this is a loop back IP. To change this, replace 127.0.0.1 with 0.0.0.0 in your server settings. For example, change 127.0.0.1:8000 to 0.0.0.0:8000.

#### Accessing Your host address from Your Phone
Now that everything is set up, you can access the host address from your phone. Open your phone's web browser and enter your computer's IP address followed by the port number of your server. For example, if your computer's IP address is `192.168.1.40` and your server is running on port `8080`, you would enter `192.168.1.40:8080` into your phone's browser.

And that's it! You can now access a localhost address of your computer from your phone by simply connecting to its wifi, this can be very helpful for testing applications you're developing. Hope this was helpful.