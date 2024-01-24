---
title: "Access localhost from mobile phone when connected to computer wifi"
description: "The first step is to find the IP address of your computer. This is a unique identifier for your device on the network. On Windows, open Command Prompt and type:
"
image: "images/post/post-13.png"
date: 2023-11-24T18:19:25+06:00
categories: ["programming"]
tags: ["localhost", "ubuntu"]
type: "reguler" # available types: [featured/regular]
draft: false
---

Being able to test your website or application on your phone while developing it on your desktop seems like a very interesting idea, right?. 

Or perhaps you're working remotely and need to access files on your home computer. 
With the right setup, you can do all of these things and more. But how does it work? We'll go through that in this article.

To begin, you will need to connect both your computer and mobile phone to the same Wi-Fi network. Once they are connected, you can find the IP address of your computer by a simple command in the terminal. This will give you the IP address of your local area network, which you will need to access your localhost on your mobile phone.

Once you have the IP address, you can test if it is working by typing it into your mobile phone's browser. If everything is set up correctly, you should be able to access your localhost server from your mobile phone. This is a convenient way to test your website or application on different devices without having to deploy it to a public server.


Let's get started...

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
You need to make sure that your web server is set up and running.

You will need to configure your server to accept connections from any IP address. By default, your server may be set to only accept connections from the default local host address (127.0.0.1), this is a loop back IP. To change this, replace 127.0.0.1 with 0.0.0.0 in your server settings. For example, change 127.0.0.1:8000 to 0.0.0.0:8000.

#### Accessing Your host address from Your Phone
Now that everything is set up, you need to connect your mobile phone to your computer's WiFi network. To do this, go to your mobile phone's settings and select the WiFi option. Look for your computer's WiFi network and connect to it. You may need to enter a password if you have set one up. Or rather you can turn on your phones wifi hotspot and connect to it from your desktop.

Once you are connected to your computer's WiFi network, Open your phone's web browser and enter your computer's IP address followed by the port number of your server. For example, if your computer's IP address is `192.168.1.40` and your server is running on port `8080`, you would enter `192.168.1.40:8080` into your phone's browser.

And that's it! You can now access a localhost address a server on your computer from your phone by simply connecting to its wifi. Hope this was helpful to you.
