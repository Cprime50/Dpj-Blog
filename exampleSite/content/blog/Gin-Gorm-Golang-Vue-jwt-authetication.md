---
title: "Building a fullstack application with Go Gin Gorm and Vue js jwt authentication 1"
description: "We will be setting up a Restful Api application, using Go, Gin, Gorm and we will be consumming that api with Vue js. In this section we will be writing our postgres connection"
image: "images/post/go-gin-api.jpg"
date: 2023-06-26T18:19:25+06:00
categories: ["programming", "Reguler Club"]
tags: ["go", "gin", "Vue", "Gorm"]
type: "featured" # available types: [featured/regular]
draft: false
---

Hello guys, welcome once again to my blog. This is going to be the first coding part of our `Reguler Club` tutorial where I will be sharing with you how to structure, a Golang restAPi project using Gin, connecting to a postgres database using Gorm, handling user authentication using jwt and assigning user roles. If you've missed the first section where I did a simple introduction of the software we will be building, its design and a breakdown of the technologies that we will be using, you can catch up [here](http://www.charlesdpj.com/blog/building-a-fullstack-monolith-with-go-gin-gorm-vue).


#### What is Go?
Go or Golang is a high-level open-source programming language developed by Google. Go is used to develop web applications, cloud and networking services, system softwares, games, and other types of softwares. 
Go is loved because of its support for concurrency. It has automatic memory management, otherwise called garbage collection, which makes it easy to use without much compromise on performance. It also has a clear and concise syntax. You can download Go from the [Go website](https://golang.org/). 

#### What is Gin??
For this project, we're going to be using the Gin Framework. Gin is a high-performance HTTP framework within Go. It features a Martini-like API, but with performance up to 40 times faster than Martini. It also comes with some features out of the box like routing, middleware support, rendering. We're going to be using Gin for faster development.

#### ORM?
GORM is the go-to ORM for Golang. An ORM(Object Relational Mapping), is used in translating data representation from one type system to that of a database. It's a simple way to avoid writing raw SQL code. 

#### Database?
Postgres is a free and open-source relational database management system. You can download Postgres, but you don't need to because in this video, we're going to be hosting our database locally on Docker. Now let's get started

{{< image src="https://deadline.com/wp-content/uploads/2016/09/regular-show.jpg?w=681&h=383&crop=1" caption="Reguler show" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="modecai and rigby" webp="false" >}}

#### Setting up the environment

Get your favorite IDE, mine is VSCODE
Hopefully you have go installed by now
Confirm installation by using this command in your terminal:
{{< highlight bash >}}
 go version
{{< /highlight >}}

Let's start by creating our project folder.
{{< highlight bash >}}
 mkdir regclub
 cd regclub
{{< /highlight >}}

Our projects setup directory will look something like this:
{{< highlight bash >}}
|-- Database # hold files interacting with database connection
|-- forms # hold functions to validate json payload
|-- migrations # hold functions that will handle seeding data to the database
|-- models # hold functions that interact with the database
|-- routes # holds all of our apps endpoints
|-- util # holds files that handle security
|-- main.go # holds the connection to the server
|-- .env # holds our private values
|-- docker-compose.yml # holds our local database
{{< /highlight >}}

Next we need to a way to gather and track all the packages we are using, this is managed very easily in go by running a simple command in the terminal. You should edit to use your own github name and project name.
{{< highlight bash >}}
 go mod init github.com/Cprime50/regclub
{{< /highlight >}}
This creates a go.mod and go.sum file with a list of packages.

#### Create a postgreSQL docker container
I mentioned in the last [section](http://www.charlesdpj.com/blog/building-a-fullstack-monolith-with-go-gin-gorm-vue), that we would be using docker to host our postgres database. So you need to have docker installed on your system. This comes with docker-compose by default.

Create a docker-compose.yml file in the root of your project directory. The file will be used to define and run a docker container for our postgres database:
{{< highlight bash >}}
touch docker-compose.yml
{{< /highlight >}}

*docker-compose.yml*

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1">}}
 version: '3'

services:

  # start Postgres, and ensure that data is stored to a mounted volume
  postgres:
    image: 'postgres:latest'
    ports:
      - 5432:5432
    restart: always
    env_file:
      - ./.env
    volumes:
        - postgres:/var/lib/postgresql/data

volumes:
  postgres:
{{< /highlight >}}

1. version : specifies the version of docker-commpose file format being used in our case version '3'. 
2. services: The services or container that will be a part of our application. Here we are only using one service but you can have multiple services for a single application. I may add extra services as we go.
   1. postgres: This is our postgres server, it will run a postgres server based on the credentials we will provide below.
      1. image : Specifies the docker image used for the postgres service. in this case the latest version of postgres
      2. ports: This maps the containers port to a specific host we want it to run on in our machine. In our case we mapped our local port 5432 to postgres default port of 5432. 
      3. restart: This species whether the container should restart automatically if it stops for any reason. In our caseit is set to yes.
      4. env_file: we are storing all of our credentials in an .env file, so this is used to load the credentials required by the postgres container.
      5. volumes: This defines a named volume called "postgres" and maps it to the '/var/lib/postgresql/data' directory within the container. This is used to store the postgres data so it's not lost when the container stops running or is recreated.
3. volumes: This section defines Docker volumes that can be used by the servicess. In this case we define our "postgres" volume


Next let's create a `.env` file at the root of our projects directory to hold our credentials required by the postgres image.
{{< highlight bash >}}
touch .env
{{< /highlight >}}

*.env*
{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1">}}
#docker db
POSTGRES_PASSWORD=password123
POSTGRES_USER=postgres
POSTGRES_DB=RegulerClub

PORT=8000
CLIENT_ORIGIN=http://localhost:3000
{{< /highlight >}}

This is very important, our `.env` holds very secretive information we want to keep away from the public so we would dont want this file getting pushed to github. Let's create a `.gitignore` file to make this doesnt happen.

*.gitignore*
{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=1">}}
# Binaries for programs and plugins
*.exe
*.exe~
*.dll
*.so
*.dylib

# Test binary, built with `go test -c`
*.test

# Output of the go coverage tool, specifically when used with LiteIDE
*.out

# Dependency directories (remove the comment below to include it)
# vendor/
.DS_Store
TODO.txt
logs.txt
.idea/
secret.md
dev.env
*.env
{{< /highlight >}}

Any files you don't want getting pushed to github should be put here.

Next, let's test out our postgres container. Launch your docker application on your computer then insert the following command in your terminal:
{{< highlight bash >}}
docker-compose up -d --build
{{< /highlight >}}

{{< highlight bash >}}
docker-compose up -d
{{< /highlight >}}

You can stop the postgres container aswell with this command:
{{< highlight bash >}}
docker-compose up down
{{< /highlight >}}

Hang on, we're almost about to start writing some GO code. Let's import some important packages first, the `Gin framework`, `Godotenv` library for loading environmental variables from our `.env` file, `Gorm` is our ORM library, `Gorm postgres driver` and `Go-jwt` package.

{{< highlight bash >}}
// a simple Go Http web framework
go get github.com/gin-gonic/gin
// package to laod .env file
go get	github.com/joho/godotenv
// ORM (object relational mapping) library for Go
go get -u gorm.io/gorm
// gorm driver package for connecting a postgres database
go get -u gorm.io/driver/postgres
// jwt-go package
go get -u github.com/golang-jwt/jwt/v5
{{< /highlight >}}

Gorm can also be used with other populer `SQL` databases such as `mysql`, `sqlite`, `sql server`, the set up is quite similer to what we will do here, refer to the [gorm documentation](https://gorm.io/) for more information on that.

#### Connecting our database
We want to establish a connection from our Go application `regclub`  to the postgreSQL server, using the GORM library. Let's start by adding some credentials to our `.env` file:
{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=8">}}
# Database credentials
DB_HOST="localhost"
DB_USER=postgres
DB_PASSWORD=password123
DB_NAME=RegulerClub
DB_PORT=5432
{{< /highlight >}}

Let's create a file that will hold the connection to our database:
{{< highlight bash >}}
// create a database folder and a database.go file inside it
mkdir database
touch database/database.go
{{< /highlight >}}

Add the following code into the `database.go` file to connect our Go application `regclub` :

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1">}}
package database

import (
	"fmt"
	"log"
	"os"

	"gorm.io/driver/postgres"
	"gorm.io/gorm"
)

var Db *gorm.DB

func InitDb() *gorm.DB {
	Db = connectDB()
	return Db
}

func connectDB() *gorm.DB {
	var err error
	host := os.Getenv("DB_HOST")
	username := os.Getenv("DB_USER")
	password := os.Getenv("DB_PASSWORD")
	dbname := os.Getenv("DB_NAME")
	port := os.Getenv("DB_PORT")

	dsn := fmt.Sprintf("host=%s user=%s password=%s dbname=%s port=%s sslmode=disable", host, username, password, dbname, port)
	db, err := gorm.Open(postgres.Open(dsn), &gorm.Config{})

	if err != nil {
		log.Fatal("Failed to connect to the Database :", err)
		return nil
	}
	log.Println("Connected Successfully to the Database")
	return db
}

func DbClose() {
	// Get generic database object sql.DB to use its functions
	sqlDB, err := Db.DB()
	if err != nil {
		log.Fatalln(err)
	}
	sqlDB.Close()
}
{{< /highlight >}}

*Explanation*
1. package database: This just means our Go file is part of the "database" package.
2. import statements: - `fmt:` is used for formatted I/O
                        - `log` is used for logging
                        - `os` is used to interact with the operating system such as getting environmental variables
                        - `gorm.io` is our orm library and `gorm.io/driver/postgres` is a gorm driver for postgreSQL
3. Global variable: - var Db *gorm.DB stores the database connection
4. InitDb Function:
                    - Initializes the datbase connection and returns the *gorm.Db object
                    - it calls the connectDB function to establish the database connection
5. connectDB Function: - This function creates a connection to the PostgreSQL database by reading the postgres connection parameters (host, username, password, dbname, port) from our `.env` file. It then constructs the data source name (DSN) using this three parameters, if a successful connection is formed it returns the GORM database object.
6. DbClose function: This function is for closing the database connection when it's no longer needed. 

#### Connecting to our server with Gin
Let's get started running our application to see if it works.
Create a main.go file that will load our `.env` file, database connection and our web server config.
Make sure you are in your projects root directory

{{< highlight bash >}}
touch main.go
{{< /highlight >}}

Add the following code to it:
{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1">}}
package main

import (
	"context"
	"log"
	"net/http"
	"os"
	"os/signal"
	"syscall"
	"time"

	"github.com/Cprime50/regclub/database" // edit to your own package directory
	"github.com/gin-gonic/gin"
	"github.com/joho/godotenv"
)

func main() {
	// load env file
	loadEnv()

	// load db config and connection
	loadDatabase()

	// close db
	defer database.DbClose()

	// start server
	serveApplication()
}

func loadEnv() {
	err := godotenv.Load(".env")
	if err != nil {
		log.Fatal("Error loading .env file", err)
	}
	log.Println("dev.env file loaded successfully")
}

func loadDatabase() {
	database.InitDb()
}

func serveApplication() {
	router := gin.Default()

	srv := &http.Server{
		Addr:    ":8082",
		Handler: router,
	}

	go func() {
		// service connections
		if err := srv.ListenAndServe(); err != nil && err != http.ErrServerClosed {
			log.Fatalf("listen: %s\n", err)
		}
		//log.Println("server running on https://localhost:8082")
	}()

	// Wait for interrupt signal to gracefully shutdown the server with
	// a timeout of 2 seconds.
	quit := make(chan os.Signal)
	// kill (no param) default send syscanll.SIGTERM
	// kill -2 is syscall.SIGINT
	// kill -9 is syscall. SIGKILL but can"t be catch, so don't need add it
	signal.Notify(quit, syscall.SIGINT, syscall.SIGTERM)
	<-quit
	log.Println("Shutdown Server ...")

	ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
	defer cancel()
	if err := srv.Shutdown(ctx); err != nil {
		log.Fatal("Server Shutdown:", err)
	}
	// catching ctx.Done(). timeout of 2 seconds.
	select {
	case <-ctx.Done():
		log.Println("timeout of 2 seconds.")
	}
	log.Println("Server exiting")
}
{{< /highlight >}}

The `main` function is the entry point of our application. Here we call several other functions inside it and then start the server.

`loadEnv` function loads environmental variables from our `.env` by using the Godotenv package.

`loadDatabase` Function initializes the datbase connection by calling the InitDb function from our database package

`serveApplication` Function sets up the Gin router, creates a HTTP server. It starts the server with a goroutine using srv.ListenAndServe()
from the go net/http package, and gracefully shutsdown the server with a timeout of 2secs if a signal to shutdown is received.

We can now test the connection by running the `go run` command, make sure your docker database is up and running.
{{< highlight bash >}}
    go run main.go
{{< /highlight >}}

Let's create a simple route to test things out a bit. Add this to your code to the `serveApplication()` function in main.go. You can remove it after, as it's not going to be useful, we are only using it to test out our server.
{{< highlight go >}}
    func serveApplication() {
	router := gin.Default()
    router.GET("/", func(c *gin.Context) {
		time.Sleep(2 * time.Second)
		c.String(http.StatusOK, "Welcome to Reguler Club Server")
	})
    
	srv := &http.Server{
		Addr:    ":8082",
		Handler: router,
	}
}
{{< /highlight >}}

Your updated code should look like this:
{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=1">}}
package main

import (
	"context"
	"log"
	"net/http"
	"os"
	"os/signal"
	"syscall"
	"time"

	"github.com/Cprime50/regclub/database" // edit to your own package directory
	"github.com/gin-gonic/gin"
	"github.com/joho/godotenv"
)

func main() {
	// load env file
	loadEnv()

	// load db config and connection
	loadDatabase()

	// close db
	defer database.DbClose()

	// start server
	serveApplication()
}

func loadEnv() {
	err := godotenv.Load(".env")
	if err != nil {
		log.Fatal("Error loading .env file", err)
	}
	log.Println("dev.env file loaded successfully")
}

func loadDatabase() {
	database.InitDb()
}

func serveApplication() {
	router := gin.Default()
    router.GET("/", func(c *gin.Context) {
		time.Sleep(2 * time.Second)
		c.String(http.StatusOK, "Welcome to Reguler Club Server")
	})

	srv := &http.Server{
		Addr:    ":8082",
		Handler: router,
	}

	go func() {
		// service connections
		if err := srv.ListenAndServe(); err != nil && err != http.ErrServerClosed {
			log.Fatalf("listen: %s\n", err)
		}
		//log.Println("server running on https://localhost:8082")
	}()

	// Wait for interrupt signal to gracefully shutdown the server with
	// a timeout of 2 seconds.
	quit := make(chan os.Signal)
	// kill (no param) default send syscanll.SIGTERM
	// kill -2 is syscall.SIGINT
	// kill -9 is syscall. SIGKILL but can"t be catch, so don't need add it
	signal.Notify(quit, syscall.SIGINT, syscall.SIGTERM)
	<-quit
	log.Println("Shutdown Server ...")

	ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
	defer cancel()
	if err := srv.Shutdown(ctx); err != nil {
		log.Fatal("Server Shutdown:", err)
	}
	// catching ctx.Done(). timeout of 2 seconds.
	select {
	case <-ctx.Done():
		log.Println("timeout of 2 seconds.")
	}
	log.Println("Server exiting")
}
{{< /highlight >}}

Access the endpoint with curl using:
{{< highlight bash >}}
curl -X GET http://localhost:8082/
{{< /highlight >}}

#### Data modeling and database migration with gorm
In this section we will be creating our User and Role models using Gorm. We will also run migrations to seed database schemas and a bit of data into the database.

Data modeling refers to defining of the structure and organisation of data to be stored in our database. In Go, data modeling is often done using structs, these structs represent datbase tables and fields in the struct correspond to columns in the table. ORM's like GORM make it easy to map these structs to the database without writing any or writing very minimal sql.

Datbase Migration simply refers to managing changes to a database schema over time. It involves applying incrementaland reversible updates to the database schema, such as adding tables altering columns or modifying indexes. It ensures consistency in database structure as our application changes.

Now that we understand what database modeling and migration means, let's start working on our User and Role model.

Create a new model directory and a user.go file:
{{< highlight bash >}}
mkdir model
touch model/user.go
{{< /highlight >}}

Will be back to finish this tutorial as I am now off to slack off wooo hoooo

{{< image src="https://qph.cf2.quoracdn.net/main-qimg-5f10a18f257ce2379ee188e9eb3c9ddd" caption="Reguler show" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="modecai and rigby" webp="false" >}}