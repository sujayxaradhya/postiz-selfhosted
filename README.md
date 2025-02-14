# Postiz Self-Hosted Setup

This repository provides a Docker Compose setup for self-hosting [Postiz](https://postiz.com/) the best social media schedulling and management tool. The configuration is designed to be easy to use and customizable for local development or small-scale deployments.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Running the Application](#running-the-application)
5. [Accessing the Application](#accessing-the-application)
6. [Stopping the Application](#stopping-the-application)
7. [Customization](#customization)

---

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Docker**: [Install Docker](https://docs.docker.com/get-docker/)
- **Docker Compose**: [Install Docker Compose](https://docs.docker.com/compose/install/)

---

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/sujayxaradhya/postiz-selfhosted.git
   cd postiz-selfhosted
   ```

2. Create a `.env` file in the root directory of the project. Use the template below to configure your environment variables:
   ```env
   # Postiz Configuration
   POSTIZ_PORT=your-defined-port
   BACKEND_PORT=your-defined-port
   JWT_SECRET=your-random-secret-string

   # PostgreSQL Configuration
   POSTGRES_USER=postiz-user
   POSTGRES_PASSWORD=postiz-password
   POSTGRES_DB=postiz-db-local
   POSTGRES_PORT=5432

   # Redis Configuration
   REDIS_PORT=6379
   ```

3. Ensure that the ports specified in the `.env` file do not conflict with other services running on your machine.

---

## Configuration

The `.env` file contains all the essential environment variables required for the application to run. Below is a description of each variable:

| Variable          | Description                                      | Example Value           |
|-------------------|--------------------------------------------------|-------------------------|
| `POSTIZ_PORT`     | Port for the main entry point of Postiz          | `port`                 |
| `BACKEND_PORT`    | Internal port for the backend service            | `port`                 |
| `JWT_SECRET`      | Secret key for JSON Web Token encryption         | `your-random-secret-string` |
| `POSTGRES_USER`   | Username for the PostgreSQL database             | `postiz-user`          |
| `POSTGRES_PASSWORD` | Password for the PostgreSQL database           | `postiz-password`      |
| `POSTGRES_DB`     | Name of the PostgreSQL database                  | `postiz-db-local`      |
| `POSTGRES_PORT`   | Port for the PostgreSQL service                  | `5432`                 |
| `REDIS_PORT`      | Port for the Redis service                       | `6379`                 |

**Important**: Do not commit your `.env` file to version control. It contains sensitive information such as database credentials and secrets.

---

## Running the Application

1. Start the services using Docker Compose:
   ```bash
   docker compose up -d
   ```

2. Verify that all containers are running:
   ```bash
   docker ps
   ```

3. Check the logs for any errors:
   ```bash
   docker compose logs
   ```

---

## Accessing the Application

Once the services are up and running, you can access the application at the following URLs:

- **Frontend**: `http://localhost:${POSTIZ_PORT}`
- **API**: `http://localhost:${POSTIZ_PORT}/api`

Use the value of `POSTIZ_PORT` if you customized it in the `.env` file.

---

## Stopping the Application

To stop the services, run:
```bash
docker compose down
```

This will stop and remove all containers, but the data stored in volumes (e.g., PostgreSQL and Redis) will persist.

---

## Customization

### Changing Ports
If the default ports conflict with other services on your machine, update the `.env` file with new values for `POSTIZ_PORT`, `POSTGRES_PORT`, and `REDIS_PORT`.

### Scaling Services
You can scale specific services by modifying the `POSTIZ_APPS` environment variable in the `.env` file. For example:
- Frontend only: `POSTIZ_APPS="frontend"`
- Backend only: `POSTIZ_APPS="backend"`
