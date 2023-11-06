---
title: "How to Deploy Your Django App For Free on Fly.io"
description: "Fly.io is a Platform as a Service (PaaS) that offers web hosting with a distinctive approach. Many other traditional PaaS providers typically resell services from major cloud providers like AWS or Google Cloud, Fly.io takes a different approach to hosting by hosting applications on top of physical dedicated servers globally. They have a wide network of dedicated servers world wide with over 20 locations to choose from, users can have the choice to pick one closest to them."
image: "images/post/django.png"
date: 2022-06-24T18:19:25+06:00
categories: ["programming"]
tags: ["tech", "coding", "Django"]
type: "regular" # available types: [featured/regular]
draft: false
sitemapExclude: false
---

Deploying a Django app can feel like a daunting task, often turning what should be a triumphant moment into a source of frustration. Unlike the relatively straightforward process of hosting static websites, deploying a dynamic Django application comes with its own set of challenges. However, I will show you how you can deploy Django easily in less than 5minutes on a populer hodting platform called [fly.io](https://fly.io) fly. Yes that's right,  make your django project fly into the clouds. I will break down the deployment process into manageable steps so that you do not get lost.

#### What is fly.io
[fly.io](https://fly.io) is a Platform as a Service (PaaS) that offers web hosting with a distinctive approach. Many other traditional PaaS providers typically resell services from major cloud providers like AWS or Google Cloud, Fly.io takes a different approach to hosting by hosting applications on top of physical dedicated servers globally. They have a wide network of dedicated servers world wide with over 20 locations to choose from, users can have the choice to pick one closest to them.
[Fly](https://fly.io) is also very cheap and even offer a free plan for users who want to test out their applications. In this article we will be discussing how we can liverage the free offer from fly and host our django application.

[Flys](https://fly.io)Flys free plan comes with the following:


    Up to 3 shared-cpu-1x 256 MB VMs

    3GB persistent volume storage (total)

    160GB outbound data transfer

This is very well enough for us to test our application.


> Code is read more than it is written. An individual block of code takes moments to write, minutes or hours to debug, and can last forever without being touched again.

#### Let's get started
Here, we will be building a simple django app and deploying it to [fly.io](https://fly.io).

First you should have python installed I assume? if you don't you can download it from [here](https://www.python.org/downloads/).

Let's create a simple django project called fly-django. Run the following command accordingly the way you see them in order not to make any mistakes.


Go to your terminal and cd into your desktop folder, then run the following command to create a new folder:
```python
    $ mkdir fly-django
```

Next cd into the project folder:
{{< highlight python >}}
    $ cd fly-django
{{< /highlight >}}

Now we're done with that let's create a virtual environment create a virtual environment:
{{< highlight python >}}
#Windows
    $ python -m venv .venv

#macOS
    $ python3 -m venv .venv 
{{< /highlight >}}

znow Let's activate the environment, make sure to run this in the root folder that is the fly-django folder and not the fly-app folder otherwise u may get an error:
{{< highlight python >}}
#Windows
    $ .venv\Scripts\Activate.ps1

#macOS
    $ source .venv/bin/activate
{{< /highlight >}}



this should work, just make sure to cd out of the .venv once you're done by running.
{{< highlight pythonhtml >}}
#Windows
    $ cd..
{{< /highlight >}}


Next install Django in your project folder by running:
{{< highlight python >}}
#Windows
    (.venv) $ python -m pip install django

#mac os
    (.venv) $ python3 -m pip install
{{< /highlight >}}

Next let's start a our fly-django project by running the startproject command
{{< highlight pythonbsah >}}
    (.venv) $ django-admin startproject fly-django
{{< /highlight >}}

You'll notice a list of new files and folders have been created in your project folder, this should include our fly-django folder, a settings.py and manage.py file inside the folder.

Now let's create our app, run  this command:
{{< highlight python >}}
    (.venv) $ python manage.py startapp fly-app
{{< /highlight >}}

Add our new fly-app to your list of installed apps in your settings.py file:

{{< highlight python >}}
#fly-django/settings.py
    INSTALLED_APPS = [
        "django.contrib.admin",
        "django.contrib.auth",
        "django.contrib.contenttypes",
        "django.contrib.sessions",
        "django.contrib.messages",
        "django.contrib.staticfiles",
        "fly-app",  #new
    ]
{{< /highlight >}}

Next run the migrate command this will create an sqlite database for our app:
{{< highlight python >}}
    (.venv) $ python manage.py migrate
{{< /highlight >}}

We're done creating our app now let's view what it looks like by running our local server:
{{< highlight python >}}
    (.venv) $ python manage.py runserver
{{< /highlight >}}

Visit the local host url: [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your web browser to see the Django welcome page. You should see a green rocket and message saying "The install worked succesffully! Congratulations!"

#### Deploying our app
Firstly we need to get all our project dependencies in one file, this is very important. I've found that most of the errors I've experienced when deploying with django had to do with my dependencies. Our Cloud machine may have a hard time installing the packages we've listed there and this can cause our deployment to fail.
Run:
{{< highlight python >}}
   pip freeze > requirements.txt
{{< /highlight >}}

Make sure to remove any package you're sure you didnt use inn your app. This is why it is best to always have a virtual environment running before installing any package in our app, so we dont get our dependencies mixed up with other packages in our local computer.

If you're using a postgres database, make sure you have psycopg2-binary
If not
Run:
{{< highlight python >}}
    pip install psycopg2-binary
{{< /highlight >}}

We need to install flyctcl. Flyctl is a fly command line interface that makes it easy for us to deploy directly to `fly.io` from our terminal

To install run the command:
`Mac Os`
{{< highlight python >}}
    brew install flyctl
{{< /highlight >}}

OR

{{< highlight python >}}
    curl -L https://fly.io/install.sh | sh
{{< /highlight >}}

`Linux`
{{< highlight python >}}
    curl -L https://fly.io/install.sh | sh
{{< /highlight >}}

`Windows`
Run on powershell:
{{< highlight python >}}
pwsh -Command "iwr https://fly.io/install.ps1 -useb | iex"
{{< /highlight >}}

You will be prompted to sign up or if you already have an account, sign in.

If you don't have an account
Run:
{{< highlight python >}}
    fly auth signup
{{< /highlight >}}

You can sign up with your email or your github account.

If you already have an account
Run
{{< highlight python >}}
fly auth login
{{< /highlight >}}

##### `Next step:`
Run the command:
{{< highlight python >}}
    fly launch
{{< /highlight >}}

You will be prompted a couple of questions you will need to answer

Choose any name of your choice
{{< highlight python >}}
    ? Choose an app name (leave blank to generate one): fly-app
{{< /highlight >}}

Select a Location closest to you
{{< highlight python >}}
   ? Choose a region for deployment: Ashburn, Virginia (US) (iad)
{{< /highlight >}}

You can select the option to set up a postgres database but I sugest responding no to this one. We dont want to be getting any unecessary errors.
You can set up a free postgres database on [render](https://render.com)

{{< highlight python >}}
Created app fly-app in organization personal
Set secrets on fly-app: SECRET_KEY
Creating database migrations
Wrote config file fly.toml
? Would you like to set up a Postgresql database now? No
{{< /highlight >}}

Select anyone of that best fits your need but since this is only a test deployment we can use the smallest
{{< highlight python >}}
? Select configuration: Development - Single node, 1x shared CPU, 256MB RAM, 1GB disk
Creating postgres cluster in organization personal
Creating app...
{{< /highlight >}}

We should see a dockerfile and a fly.toml file added to our root folder. 

##### `Next step:`
Run:
{{< highlight python >}}
    fly deploy
{{< /highlight >}}

This will take a while. Hopefully it works successfully. If it doesn't then
check the fly logs for the error description for why it failed
{{< highlight python >}}
    fly logs
{{< /highlight >}}

If it works successfully then great. Your app is ready. Now run the command to view it on the web:

{{< highlight python >}}
   fly open
{{< /highlight >}}



#### Conclusion
Hosting Django on fly is quite easy once you follow the right steps. Other cloud platforms that can help you with hosting are aws, vercel, railway and pythonanywhere. While deploying a Django app may present its challenges, it's not an insurmountable task. By understanding the steps involved, following a well-structured approach and leveraging the appropriate hosting platforms you can transform the stressful process into a successful and rewarding achievement. Remember, each deployment teaches valuable lessons that contribute to your growth as a developer, making the journey as important as the destination.
