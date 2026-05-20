# Node Docker Lab 🚀

## Introduction

This project was carried out as part of my DevOps learning journey to understand how containerization works using Docker.

The goal of the project was to:
- Build a simple Node.js application
- Containerize the application using Docker
- Run the application inside a Docker container
- Access the application through a web browser
- Understand the workflow of Docker images and containers

This project helped me gain practical experience with Docker, Dockerfiles, image creation, port mapping, and container management.

---

# Technologies Used

- Node.js
- Express.js
- Docker
- NGINX (during earlier Docker practice)

---

# Project Structure

```bash
node-docker-lab/
│
├── Dockerfile
├── .dockerignore
├── package.json
├── package-lock.json
└── src/
    └── index.js
```

---

# Creating the Node.js Application

The first step was creating a simple Node.js application using Express.

## Initialize the Project

The project was initialized using:

```bash
npm init -y
```

This generated the `package.json` file for managing project dependencies and configurations.

---

## Install Express

Express was installed as the web framework for the application:

```bash
npm install express
```

---

## Application File

A `src` directory was created along with an `index.js` file containing the application logic.

The application listens on port `3000` and returns a simple message when accessed from the browser.

Example application code:

```javascript
const express = require('express');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello from Dockerized Node.js App 🚀');
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

---

# Running the Application Locally

Before containerizing the application, it was tested locally to confirm it was working properly.

```bash
node src/index.js
```

The application became accessible on:

```text
http://localhost:3000
```

---

# Dockerizing the Application

After confirming the application worked locally, the next step was containerization using Docker.

---

# Creating the Dockerfile

A `Dockerfile` was created in the project root directory.

The Dockerfile performs the following tasks:

- Uses the official Node.js Alpine image as the base image
- Creates a working directory inside the container
- Copies dependency files
- Installs project dependencies
- Copies application files into the container
- Exposes port `3000`
- Starts the Node.js application

Dockerfile used:

```dockerfile
FROM node:24-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "src/index.js"]
```

---

# Creating the .dockerignore File

A `.dockerignore` file was also created to prevent unnecessary files from being copied into the Docker image.

Contents:

```bash
node_modules
npm-debug.log
```

This helps reduce image size and improve build efficiency.

---

# Building the Docker Image

The Docker image was built using:

```bash
docker build -t node-lab .
```

Explanation:
- `docker build` creates the image
- `-t` assigns a name to the image
- `node-lab` is the image name
- `.` tells Docker to use the current directory

---

# Running the Docker Container

After building the image successfully, the container was started using:

```bash
docker run -d -p 3000:3000 --name nodeapp node-lab
```

Explanation:
- `-d` runs the container in detached mode
- `-p 3000:3000` maps the local machine port to the container port
- `--name nodeapp` assigns a custom container name
- `node-lab` specifies the image to use

---

# Verifying the Running Container

To verify that the container was running:

```bash
docker ps
```

This displayed the active running container and the exposed ports.

---

# Accessing the Application

After the container started successfully, the application became accessible from the browser through:

```text
http://localhost:3000
```

The browser displayed the message from the Node.js application, confirming successful containerization.

---

# Managing the Container

## Stop the Container

```bash
docker stop nodeapp
```

---

## Restart the Container

```bash
docker start nodeapp
```

---

## Remove the Container

```bash
docker rm nodeapp
```

---

# Challenges Encountered

During the project, a port conflict issue was encountered because port `8080` was already occupied by another service on the system.

This was resolved by:
- identifying the port conflict
- switching to another available port when necessary

The project also helped in understanding the difference between:
- Docker images
- Docker containers
- local files vs container filesystems

---

# Key Concepts Learned

Through this project, the following DevOps and Docker concepts were practiced:

- Docker Images
- Docker Containers
- Dockerfile
- Port Mapping
- Container Lifecycle
- Node.js Containerization
- Image Rebuilding
- Running Applications Inside Containers

---

# Conclusion

This project provided hands-on experience with Docker and containerization workflows. It strengthened my understanding of how applications can be packaged into portable containers that run consistently across different environments.

The project also served as a foundation for more advanced DevOps concepts such as:
- Docker Compose
- CI/CD pipelines
- Kubernetes
- Multi-container applications

