---
title: "Migrating an SQL Database to Django: A Step-by-Step Guide"
description: "To get started, create a new Django project using the django-admin startproject command. This will set up the basic project structure and configuration files necessary for our migration."
image: "images/post/post12.png"
date: 2022-06-24T18:19:25+06:00
categories: ["programming"]
tags: ["tech", "coding", "Django"]
type: "regular" # available types: [featured/regular]
draft: true
---

### How to load sql file django database
Know that unlike importing and exporting a json data with django inbuilt command:
{{< highlight python >}}
python manage.py loaddata< dataload.json
python manage.py dumpdata> datadump.json
{{< /highlight >}}

with 
Use the command: 
[cat filename.sql | python manage.py dbshell](https://stackoverflow.com/questions/48737478/how-to-load-sql-file-with-manage-py)
[How to store a dictionary in a Django database model's field?](https://stackoverflow.com/questions/68248414/how-to-store-a-dictionary-in-a-django-database-models-field)
[Exporting and importing data in Django using pg_dump in postgresql, mysqldump in mysql, dumpdata and loaddata commands in Django](https://django.cowhite.com/blog/exporting-and-importing-data-in-django-using-pg_dump-in-postgresql-mysqldump-in-mysql-dumpdata-and-loaddata-commands-in-django/)


#### What is fly.io
Fly.io is a Platform as a Service (PaaS) that offers web hosting with a distinctive approach. Many other traditional PaaS providers typically resell services from major cloud providers like AWS or Google Cloud, Fly.io takes a different approach to hosting by hosting applications on top of physical dedicated servers globally. They have a wide network of dedicated servers world wide with over 20 locations to choose from, users can have the choice to pick one closest to them.
Fly is also very cheap and even offer a free plan for users who want to test out their applications. In this article we will be discussing how we can liverage the free offer from fly and host our django application.

Flys free plan comes with the following:

Up to 3 shared-cpu-1x 256 MB VMs
3GB persistent volume storage (total)
160GB outbound data transfer

This is very well enough for us to test our application.


> Code is read more than it is written. An individual block of code takes moments to write, minutes or hours to debug, and can last forever without being touched again.

#### Conclusion
Hosting Django on fly is quite easy once you follow the right steps. Other cloud platforms that can help you with hosting are aws, vercel, railway and pythonanywhere. While deploying a Django app may present its challenges, it's not an insurmountable task. By understanding the steps involved, following a well-structured approach and leveraging the appropriate hosting platforms you can transform the stressful process into a successful and rewarding achievement. Remember, each deployment teaches valuable lessons that contribute to your growth as a developer, making the journey as important as the destination.