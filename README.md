# data-app   
https://lavinia-81.github.io/data-app/      

## Overview   
This project demonstrates how to connect a JavaScript Front-End and a Nodejs server Back-End, running in Docker with a MongoDB database.   

## Technologies Used   
- **Front-end:** JavaScript   
- **Back-end:** Node.js   
- **Database:** MongoDB (Docker container)   
- **CI/CD:** Jenkins   
- **Cloud:** AWS   

## Steps to Set Up   

1. ** Build the JavaScript Application and Nodejs Server: **   
    * Commit the JavaScript application and Nodejs Server to Git. *
    * The application can run if using the following command on bash terminal: *
     ```
     node server.js
     ```
    * The application will be available on port 3000. *

 2. ** Create a MongoDB Images: **   
     * Creeate Mongo and Mongo-Express images by acces the folow commands: *
     ```
     docker pull mongo:4.4
     ```
     ```
     docker pull mongo-express
     ```
 3. ** Create a network to connect both Docker images: **
     ```
     docker network create mongo-network
     ```
 4. ** Configurate MongoDB image: **
    ```
    docker run -d \
      -p 27017:27017 \
      -e MONGO_INITDB_ROOT_USERNAME=admin \
      -e MONGO_INITDB_ROOT_PASSWORD=password \
      --net mongo-network \
      --name mongodb \
      mongo:4.4
    ```

5. ** Configurate Mongo-Express image: **
    ```
    docker run -d \
      -p 8081:8081 \
      -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
      -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
      -e ME_CONFIG_MONGODB_SERVER=mongodb \
      --net mongo-network \
      --name mongo-express \
      mongo-express
    ```

6. ** Bild a Image Enviroment Blueprint in Dockerfile: **   
    * FROM node:18-alpine... *
    * Bild an images based on Dockerfile: *
    ```
    docker build -t app.test:1.3 .
    ```

7. ** Pushed the docker images to a private repository in AWS: **   
    * After build and configurate the image will be push to a private repository. *
    ```
    docker push 12345678910.dkr.ecr.us-west-1.amazonaws.com/app.test:1.3
    ```

8. ** Running the application with docker-compose and a yaml file. **
    * There will be an image running for the private repository and two images running from a public one. Those images communicate with each other to run the application. *
   
    * Start compose: *
    ```
    docker-compose -f mongo.yaml up
    ```
    
    * Stop compose: *
    ```
    docker-compose -f mongo.yaml down
    ```
    
9. ** Using Docker Volumes to persist data between container. **
    *To avoid losing data each time the application stops, use Docker volumes: *
    
    * Start volumes: *
    ```
    docker-compose -f docker-compose.yaml up
    ```
    
    * Stop volumes: *
    ```
    docker-compose -f docker-compose.yaml down
    ```



