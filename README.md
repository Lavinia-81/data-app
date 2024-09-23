# data-app   
https://lavinia-81.github.io/data-app/   


Connecting a JavaScript and Nodejs application to a Docker container with a MongoDB database and starting development.   

## Overview   
This project demonstrates how to connect a JavaScript front-end with a Node.js back-end, running in a Docker container with a MongoDB database.   

## Technologies Used   
- **Front-end:** JavaScript   
- **Back-end:** Node.js   
- **Database:** MongoDB (Docker container)   
- **CI/CD:** Jenkins   
- **Cloud:** AWS   

## Steps to Set Up   

1. **Build the JavaScript Application:**   
   - Commit the JavaScript application to Git. This triggers a continuous integration process with Jenkins, which produces artifacts for the JavaScript application.   

2. **Create a Docker Image:**   
   - Jenkins will create a Docker image from the JavaScript artifacts.   

3. **Push the Docker Image:**   
   - Once the image is created by the Jenkins build, it is pushed to a private repository in AWS.   

4. **Configure the Next Steps:**   
   - This can be done using Jenkins or other scripts and tools.   

5. **Deploy the Docker Images:**   
   - The Docker images need to be deployed on a development server. This server pulls images from the private repository, including the JavaScript application image and the MongoDB image.   

6. **Run the Containers:**  
   - There will be two containers running on the development server—one for the private container and one for the public development container. These containers communicate with each other to run the application.  
   - 

## Running MongoDB and Mongo Express

### Configurate MongoDB
```
docker run -d \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password \
  --net mongo-network \
  --name mongodb \
  mongo:4.4
```

### Configurate Mongo-Express
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

### Docker Compose

# Create docker-network and Run Docker Compose
```
docker network create mongo-network
```

# Start compose
```
docker-compose -f mongo.yaml up
```

# Stop compose
```
docker-compose -f mongo.yaml down
```

