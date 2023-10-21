---
title: "Building a Go API Server with Gin and Docker"
description: "Learn how to build a Go API server with the Gin framework and containerize it using Docker. This step-by-step guide covers setting up the project, creating a Dockerfile, configuring Docker Compose, handling environment variables, and accessing your API. Start building scalable and efficient Go APIs now!"
image: "images/post/post-12.png"
date: 2023-06-24T18:19:25+06:00
categories: ["programming"]
tags: ["go", "golang", "Docker", "gin"]
type: "featured" # available types: [featured/regular]
draft: false
---


In this tutorial, we'll walk you through the process of creating a Go API server using the Gin framework and containerizing it with Docker. By the end of this guide, you'll have a fully functional Go API server running in a Docker container, complete with route handlers.

#### Prerequisites

Before we begin, make sure you have the following prerequisites installed on your system:

1. Go: You can download and install Go from the [official website](https://golang.org/).
2. Docker: Install Docker from the [Docker website](https://www.docker.com/get-started).

#### Setting Up the Project

Let's start by creating a new repository and initializing it for your project:

{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
   # Create a new repository
mkdir my-gin-api
cd my-gin-api
git init

# Initialize the project with Go modules
go mod init my-gin-api

{{< /highlight >}}


#### Installing Dependencies

Now, let's install the necessary dependencies, including the Gin framework:
{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
go get -u github.com/gin-gonic/gin
{{< /highlight >}}

#### Creating the Server

Next, we'll create the main server file `main.go`:

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
    package main

import (
	"context"
	"log"
	"net/http"
	"os"
	"os/signal"
	"syscall"
	"time"

	"github.com/gin-gonic/gin"
)

func main() {
	log.Println("Starting Server...")

	router := gin.Default()

	router.GET("/api/account", func(c *gin.Context) {
		c.JSON(http.StatusOK, gin.H{
			"message": "Hello, brosephs!",
		})
	})

	// Our server struct
	srv := &http.Server{
		Addr:    ":8080",
		Handler: router,
	}

	// Graceful shutdown
	go func() {
		if err := srv.ListenAndServe(); err != http.ErrServerClosed {
			log.Fatalf("Failed to initialize server: %v\n", err)
		}
	}()

	log.Printf("Listening on port %v\n", srv.Addr)

	// Wait for kill signal of channel
	quit := make(chan os.Signal)
	signal.Notify(quit, syscall.SIGINT, syscall.SIGTERM)

	// This blocks until a signal is passed into the quit channel
	<-quit

	// The context is used to inform the server it has 3 seconds to finish
	// the request it is currently handling
	ctx, cancel := context.WithTimeout(context.Background(), 3*time.Second)
	defer cancel()

	// Shutdown server
	log.Println("Shutting down server...")

	if err := srv.Shutdown(ctx); err != nil {
		log.Fatalf("Server forced to shutdown: %v\n", err)
	}
}
{{< /highlight >}}


This code sets up a basic Gin server that listens on port 8080 and responds to a `/api/account` endpoint.

#### Creating a Dockerfile

Now, let's create a `Dockerfile` to containerize our application:
{{< highlight bash "linenos=table,hl_lines=8 15-17,linenostart=22" >}}


Dockerfile
# Use the official Golang image as the builder
FROM golang:alpine as builder

WORKDIR /go/src/app

ENV GO111MODULE=on

RUN go get github.com/cospare/reflex

COPY go.mod .
COPY go.sum .

RUN go mod download

COPY . .

RUN go build -o ./run .

# Use a minimal Alpine image for the final container
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/

# Copy the executable from the builder
COPY --from=builder /go/src/app/run .

EXPOSE 8080
CMD ["./run"]
{{< /highlight >}}

This `Dockerfile` first builds your Go application and then packages it into a lightweight Alpine Linux container.

####  Docker Compose

To simplify the deployment process, we'll use Docker Compose to define and manage our containers. Create a `docker-compose.yml` file in the project root directory and add this to it:
{{< highlight python "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
version: "3.8"
services:
  reverse-proxy:
    # The official v2 Traefik docker image
    image: traefik:v2.2
    # Enables the web UI and tells Traefik to listen to docker
    command:
      - "--api.insecure=true"
      - "--providers.docker"
      - "--providers.docker.exposedByDefault=false"
    ports:
      # The HTTP port
      - "80:80"
      # The Web UI (enabled by --api.insecure=true)
      - "8080:8080"
    volumes:
      # So that Traefik can listen to the Docker events
      - /var/run/docker.sock:/var/run/docker.sock
  account:
    build:
      context: ./account
      target: builder
    image: account
    env_file: .env.dev
    expose:
      - "8080"
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.account.rule=Host(`bro.test`) && PathPrefix(`/api/account`)"

    environment:
      - ENV=dev
    volumes:
      - ./account:/go/src/app
    # have to use $$ (double-dollar) so docker doesn't try to substitute a variable
    command: reflex -r "\.go$$" -s -- sh -c "go run ./"
{{< /highlight >}}

This Docker Compose configuration specifies a service for our Go application. It builds the Docker image using the current directory (where your `Dockerfile` is located) and maps port 8080 inside the container to port 8080 on your host.

#### Environment Variables

To store sensitive information like API keys and other configuration settings, we'll use an environment file. Create a `.env.dev` file in the project root to store your environment variables. Don't forget to add this file to your `.gitignore` to keep it secure.

#### Setting Up Hosts

To access your application, you'll need to add an entry to your hosts file. On Windows, you can do this by opening Notepad as an administrator and opening the hosts file located at `C:\Windows\System32\drivers\etc`. Add an entry for your application's hostname:

{{< highlight bash >}}
127.0.0.1 bro.test
{{< /highlight >}}

#### Running the Application

Now, you can start your application and Traefik reverse proxy by running the following command in your project's root directory:

{{< highlight python "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
docker-compose up
{{< /highlight >}}

You can access your API at `http://bro.test:8080/api/account` or test it using tools like Postman or cURL. For example:

{{< highlight bash  "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
curl -X GET http://bro.test:8080/api/account
{{< /highlight >}}

That's it! You've successfully created a Go API server using the Gin framework, containerized it with Docker, and set up a development environment with Docker Compose. You're now ready to build and expand your API as needed.