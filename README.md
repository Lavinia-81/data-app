# Data-App
Full DevOps Pipeline • Docker • Node.js • MongoDB • AWS • Jenkins  
Live Demo: https://lavinia-81.github.io/data-app/

A complete end‑to‑end DevOps project demonstrating how to connect a JavaScript front‑end with a Node.js back‑end, containerize the entire system using Docker, orchestrate services with docker‑compose, store data in MongoDB, and push production images to AWS ECR.
This project was created as the final presentation for my DevOps course.

---

## Overview
Data-App showcases a full DevOps workflow:
- Front-end + Back-end integration
- Docker containerization
- MongoDB database running in Docker
- Docker networking
- Docker volumes for data persistence
- Custom Dockerfile for the Node.js application
- Private AWS ECR repository for image storage
- Jenkins CI/CD pipeline
- docker-compose orchestration

This project demonstrates real DevOps skills applied in a practical, production‑like environment.

---

##  Architecture
```
data-app/
│
├── frontend/              # JavaScript front-end
├── backend/               # Node.js server (server.js)
├── Dockerfile             # Custom image blueprint
├── mongo.yaml             # Compose file for MongoDB + Mongo Express
├── docker-compose.yaml    # Compose file with volumes
├── scripts/               # Helper scripts (optional)
└── README.md              # Documentation
```

---

## Technologies Used
```
Front-end
JavaScript
Static hosting (GitHub Pages)
Back-end
Node.js
Express.js
REST API
Database
MongoDB (Docker container)
Mongo Express (admin UI)
DevOps
Docker
Docker Compose
Docker Networking
Docker Volumes
AWS ECR (private repository)
Jenkins CI/CD
YAML configuration
```
---

## Local Setup
```
1️⃣ Run the Node.js Server
Commit the JavaScript front-end and Node.js back-end to Git, then run:
node server.js
The application will be available on:
http://localhost:3000
🐳 Docker Setup


2️⃣ Pull MongoDB & Mongo Express Images
docker pull mongo:4.4
docker pull mongo-express

3️⃣ Create a Docker Network
docker network create mongo-network

4️⃣ Run MongoDB Container
docker run -d \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password \
  --net mongo-network \
  --name mongodb \
  mongo:4.4
  
5️⃣ Run Mongo Express Container
docker run -d \
  -p 8081:8081 \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
  -e ME_CONFIG_MONGODB_SERVER=mongodb \
  --net mongo-network \
  --name mongo-express \
  mongo-express
 Build Custom Docker Image

6️⃣ Dockerfile (Node.js Application)
Example:
dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["node", "server.js"]

7️⃣ Build the Image
docker build -t app.test:1.3 .
Push Image to AWS ECR
After configuring AWS CLI and logging in:
docker push 12345678910.dkr.ecr.us-west-1.amazonaws.com/app.test:1.3
Your application image is now stored in a private cloud repository.
Run Application with Docker Compose

8️⃣ Start Compose
docker-compose -f mongo.yaml up

9️⃣ Stop Compose
docker-compose -f mongo.yaml down
Persist Data with Docker Volumes
To avoid losing data when containers stop:
Start with volumes:
docker-compose -f docker-compose.yaml up

Stop:
docker-compose -f docker-compose.yaml down

🔄 CI/CD Pipeline (Jenkins)
The project includes a Jenkins pipeline that:
builds the Docker image
tags it
pushes it to AWS ECR
deploys the updated container
This demonstrates a full CI/CD workflow used in modern DevOps environments.
```

---

## Purpose of This Project
This application was created as my final DevOps course project, showcasing:
- containerization
- orchestration
- cloud deployment
- CI/CD automation
- front-end + back-end integration
- database management in Docker

It represents a complete DevOps pipeline and is included in my portfolio as proof of hands‑on experience with real DevOps tools and workflows.

---

## Contributions
Contributions are welcome.
Feel free to fork the repository and submit a pull request.
