# data-app
https://lavinia-81.github.io/data-app/

Connecting a JavaScript application to a Docker container with Mongo data base image and start developing.

I use JavaScript for the front-end and Node.js for the back-end, which is connected to a local Docker container with a MongoDB database.

1. Builded the JavaScript application: Commit the JavaScript application to Git. This triggers a continuous integration process with Jenkins, which produces artifacts for the JavaScript application.
2. Create a Docker image: Jenkins will create a Docker image from the JavaScript artifacts.
3. Push the Docker image: Once the image is created by the Jenkins build, it is pushed to a private repository in AWS.
4. Configure the next steps: This can be done using Jenkins or other scripts and tools.
5. Deploy the Docker images: The Docker images need to be deployed on a development server. This server pulls images from the private repository, including the JavaScript application image and the MongoDB image.
6. Run the containers: There will be two containers running on the development server—one for the private container and one for the public development container. These containers communicate with each other to run the application.

### Start mongo:4.4
```
docker run -d
-p 27017:27017
-e MONGO_INITDB_ROOT_USERNAME=admin
-e MONGO_INITDB_ROOT_PASSWORD=password
--net mongo-network
--name mongodb
mongo:4.4
```
