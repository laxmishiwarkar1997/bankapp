# BankApp

A Spring Boot-based banking application, containerized for easy deployment using Docker and Docker Compose.

## Overview

BankApp is a demo banking application built with Spring Boot. It provides basic banking operations and is designed with modern DevOps practices in mind, supporting containerization and orchestration via Docker and Docker Compose.

## Features

- Spring Boot backend for banking operations
- MySQL database integration
- Containerized with Docker
- Multi-container orchestration with Docker Compose
- Ready for deployment and further CI/CD integration

## Deployment Instructions

Follow these steps to deploy BankApp using Docker and Docker Compose, as per command history:

### Prerequisites

- Ubuntu (or any modern Linux OS)
- Docker installed (`sudo apt install docker.io`)
- Docker Compose installed (`sudo apt install docker-compose`)
- Git installed

### Steps

1. **Update and Install Prerequisites**
   ```bash
   sudo apt-get update
   sudo apt install docker.io
   sudo apt install docker-compose
   ```

2. **Clone the Repository**
   ```bash
   git clone https://github.com/laxmishiwarkar1997/bankapp.git
   cd bankapp
   ```

3. **Build the Docker Image**
   ```bash
   docker build -t bankapp:latest .
   ```

4. **Create a Docker Network**
   ```bash
   docker network create bankapp
   ```

5. **Run MySQL Container**
   ```bash
   docker run -itd --name mysql \
     -e MYSQL_ROOT_PASSWORD=Test@123 \
     -e MYSQL_DATABASE=bankappdb \
     --network=bankapp \
     mysql:latest
   ```

6. **Run BankApp Container**
   ```bash
   docker run -itd --name bankapp \
     -e "SPRING_DATASOURCE_URL=jdbc:mysql://mysql:3306/bankappdb?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC" \
     -e SPRING_DATASOURCE_USERNAME=root \
     -e SPRING_DATASOURCE_PASSWORD=Test@123 \
     --network=bankapp \
     -p 8080:8080 \
     bankapp:latest
   ```

   _Alternatively, you can use Docker Compose:_

   ```bash
   docker-compose up --build
   ```

7. **Check if Containers are Running**
   ```bash
   docker ps
   ```

8. **Access the Application**

   The backend should be available on [http://localhost:8080](http://localhost:8080) (default port).

## Useful Commands

- View running containers: `docker ps`
- View all containers: `docker ps -a`
- View images: `docker images`
- Stop a container: `docker stop <container_name>`
- Remove a container: `docker rm <container_name>`

## Troubleshooting

- If you make changes to the Dockerfile or code, rebuild the image before restarting containers.
- Ensure the MySQL container is up before starting the Spring Boot app.
- Check container logs using: `docker logs <container_name>`

## Contributing

Contributions are welcome! Fork the repo, make changes, and submit a pull request.

## License

This project currently does not specify a license.

## Author

[laxmishiwarkar1997](https://github.com/laxmishiwarkar1997)
