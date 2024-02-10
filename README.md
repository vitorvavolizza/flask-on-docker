# Project 3 for CSCI-143

## Overview

This repository contains a Flask application configured to run in a Dockerized environment, leveraging Postgres for database management, Nginx for serving static and media files as well as acting as a reverse proxy, and Gunicorn as the WSGI HTTP Server for production environments. This setup is designed to offer a scalable and efficient way to deploy a Flask application, suitable for both development and production use.

![website demo](https://s13.gifyu.com/images/SCfGj.gif)

## Build Instructions

### Prerequisites

- Docker
- Docker Compose

Ensure Docker and Docker Compose are installed on your system.

### Setting Up the Environment

1. **Clone the repository:**

   ```sh
   git clone https://github.com/vitorvavolizza/flask-on-docker.git
   cd flask-on-docker
   ```

2. **Environment Variables:**

   Before starting the services, ensure you have the `.env.dev` and `.env.prod` files set up in your project root for development and production environments, respectively.

3. **Building and Running the Services:**

   - **For Development:**

     ```sh
     docker-compose up -d --build
     ```

     This command builds the Docker images and starts the containers. Your Flask application should now be accessible at `http://localhost:1705`.

   - **For Production:**

     ```sh
     docker-compose -f docker-compose.prod.yml up -d --build
     ```

     This command uses the `docker-compose.prod.yml` file to build and start the containers for a production environment. Your application will be accessible at `http://localhost:1707`, served via Nginx.

4. **Creating the Database:**

   After starting the Postgres container, create the database schema for development:

   ```sh
   docker-compose exec web python manage.py create_db
   ```

   Or for production:
   
   ```sh
   docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
   ```

### Usage

- **Accessing the Application:**

  - Development: Navigate to `http://localhost:1705` to view the Flask application.
  - Production: Navigate to `http://localhost:1707` to view the application served via Nginx.

- **Uploading an Image:**

  Use the `/upload` endpoint to upload an image. After uploading, the image will be accessible via the `/media/<filename>` endpoint.

### Shutting Down

To stop and remove the containers, networks, and volumes associated with your application, run the following command:

- **For Development:**

  ```sh
  docker-compose down -v
  ```

- **For Production:**

  ```sh
  docker-compose -f docker-compose.prod.yml down -v
  ```
