---
title: "SQL and RDBMS: Relational databases In A Nutshell"
description: "If you are someone who currently deals with a substantial amount of data or has previously encountered such a situation, or if you are contemplating working with extensive datasets in the future, you have or will likely be seeking effective methods for storing, organising and managing that data efficiently, which is where relational database management system(RDBMS) proves invaluable"
image: "images/post/sql-Rdbms-turorial.png"
date: 2023-05-24T18:19:25+06:00
categories: ["programming"]
tags: ["tech", "sql"]
type: "regular" # available types: [featured/regular]
draft: false
---

Imagine you have a vast collection of data, but you're unsure how to efficiently store and organize this data, well that's where databases come into play. Relational databases display this data in a table with rows and columns so it can be very easy for you to manage. When you have so much data things can become very complicated, how do you retrieve the information? or you may need to delete a particular data but there's so much of it. That's where SQL comes into play. SQL is a language specifically designed for managing and manipulating data in relational databases. It serves as a bridge between you and your database. By the time you finish reading this article, you'll gain a comprehensive understanding of SQL and databases. Whether you're a beginner or have some prior knowledge, this article will equip you with the essential skills to navigate through the realm of SQL and databases confidently. So, let's dive in and explore the magic behind effective data management!


#### Beginners guide to SQL and RDBMS: Learn how to query a database
This article revolves around learning and understanding databases, RDBMS, SQL, how to write SQL queries and understanding how they work.

> If you are someone who currently deals with a substantial amount of data or has previously encountered such a situation, or if you are contemplating working with extensive datasets in the future, you have or will likely be seeking effective methods for storing, organising and managing that data efficiently, which is where relational database management system(RDBMS) proves invaluable. So being able to query a relational database systems(RDBMS) is a great skill to aquire. SQL (Structured Query Language) enables you to do this very efficiently and easily.

#### What is SQL? you may be thinking
As we may know. Data is a fundamental component in numerous aspects of our lives, spanning accross businesses, web applications, social media platforms, and educational institutions, data such as customer or student profile information, transactional records, research findings and much more. These data needs to be stored somewhere, and this is where a database comes into the picture. 

 In this context, SQL is a programming language that enables us to work with that data. 

SQL also called SE-QU-EL stands for Structured Query Language.

It is a programming language that allows us to communicate with databases in order to manage the data contained in them. It acts as a language that bridges the gap between you and your database, enabling seamless communication and efficient data retrieval. With SQL, you can write queries to extract, insert, update, and delete data, putting you in control of your database's vast potential.


#### Operations in SQL
There are commonly four essential operations, actions or commands that can be performed using SQL. These operations includes to Create, Read, Update and Delete. In short, we can refer to these operations as CRUD.

 

###### Create:
 This operation enables us to add new records to a database. In relational databases, the row in a table is referred to as a record, while the columns are called attributes or fields.
 

###### Read:
 This operation enables us retrieve data from a database.
 

###### Update:
 This operation allows us to modify existing data within the database. For example, if we want to change the price of milk we sell, we would want to update this in our database, and this can be done using the Update operation.
 

###### Delete:
 This opearion allows us to remove specific records from the database.

#### What is Relational Database Management System (RDBMS)?

I've used this term quite a lot now and you may be wondering what it means. Not to worry, I've got you

covered.

 

Imagine it's your birthday and you have received lots of presents from freinds and family, each of these presents have a gift card with them. Each card contains information such as the name of who sent the gift card, a store name where they can be used and the value amount they are worth.

 

Now let's say you want to organize these gift cards in a way that makes it easy to find and retrieve the information contained in them.

 

A relational database is like a system that helps you store and manage your birthday gift cards efficiently. It uses tables to represent different categories of information. Each table consists of rows and columns.

 

For example, you can have a table called "Gifts" where each row represents a different gift card. The columns of the table could be "Gift ID," "Giver's Name," "Store Name," and "Value." Each gift card you have corresponds to a row in this table, and each column represents a specific piece of information about the gift card.

 

Here's an example of what our table might look:

#### History of SQL and  Relational Data Model
SQL was developed in the 1970s by IBM researchers Raymond Boyce and Donal Chamberlin. It was created following an idea on a relational database model by Edgar Frank Codd.

 

Let's take a look back to where it all began.  

 

The first computer databases were built in the 1960's. At the time alot of computer scientists were focused on improving how the databases work. Edgar Frank Codd was one of them.

{{< image src="https://upload.wikimedia.org/wikipedia/en/thumb/5/58/Edgar_F_Codd.jpg/150px-Edgar_F_Codd.jpg" caption="Edger_F_Codd" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title" webp="false" >}}


Codd was an English computer scientist employed at IBM. In 1970 Codd published his seminal paper “A Relational Model of Data for Large Shared Data Banks". This article started the era of relational databases.

At this time hierarchical databases and network databases were more prominent. They were quite inflexible and could run on only large computers.  The one-many structure of hierarchical databases was not ideal to work with complex structures of data as it could not handle multiple parents node. While the network model had provided a solution to the many-many parent-child relationship, it still had its own problems. Each and every record had to be maintained with the use of pointers.