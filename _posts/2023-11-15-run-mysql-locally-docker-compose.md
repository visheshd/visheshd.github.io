---
layout: post
title: Run MySQL locally on macOS using Docker
type: post
published: true
excerpt: "Running a MySQL server locally can be a hassle, especially when dealing with different versions and configurations."
comments: true
tags: [mysql, docker]
---

Running a MySQL server locally can be a hassle, especially when dealing with different versions and configurations. However, using Docker simplifies this process significantly. In this tutorial, we'll walk through setting up a MySQL server for local development using Docker, which is particularly useful when working with tools like Prisma and NextAuth.

### Prerequisites
- Docker installed on your machine.
- Basic understanding of Docker concepts.

### Step 1: Create a Docker-Compose File

First, we need to create a `docker-compose.yml` file which defines our MySQL service. This file ensures that MySQL runs with the desired settings.

<code>
version: '3.3'

services:
  db:
    image: mysql:latest             # Using the latest official MySQL image
    restart: always
    environment:
      MYSQL_DATABASE: 'testdb'      # Name of your database
      MYSQL_ROOT_PASSWORD: 'test'   # Root password (change for production)
      MYSQL_ROOT_HOST: '%'          # Allows root connections from any host
    ports:
      - '3306:3306'                 # Port mapping
    volumes:
      - ./<local path>:/var/lib/mysql  # Maps your local directory to the container's MySQL data directory
</code>

This file tells Docker to run the latest MySQL image, set up a database named `testdb`, and configure the necessary environment variables. It also maps port 3306 to your local machine and uses a volume for data persistence.

### Step 2: Running the MySQL Server

To start the MySQL server, navigate to the directory containing your `docker-compose.yml` file and run the following command in your terminal:

<code>docker-compose up -d</code>

This command starts your MySQL server in detached mode, meaning it runs in the background.

### Step 3: Accessing the Database

To access your new MySQL database, you can use any MySQL client with the following credentials:

- Host: `localhost`
- Port: `3306`
- User: `root`
- Password: `test`

Remember, this is for local development, so it's okay to use simple credentials. However, for a production environment, ensure to use a secure password.

### Step 4: Integrating with Prisma

If you're using Prisma, you can now connect to your local MySQL server. Update your Prisma schema file to include the MySQL connection URL:

<code>mysql://root:test@localhost:3306/testdb</code>

### Conclusion

Docker makes it incredibly easy to run a MySQL server locally, ensuring a consistent and isolated environment for your development needs. It's especially useful when working with Prisma and NextAuth for authentication mechanisms. By following these steps, you can set up a flexible and robust development environment for your projects.
