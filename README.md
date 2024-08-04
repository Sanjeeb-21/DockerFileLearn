# DockerFileLearn
# How to dockerize a node.js application 
# see the bellow command
# docker build -t <image name>
# -t means <tag> and <.> mean the file exits in the same folder
 docker build -t youtube-nodejs .
# after hit this command custom image will be created in your local ( you can see in docker desktop app under images)
# We have run the image container (youtube-nodejs)  using this command
docker run -it youtube-nodejs
# If you try to run above command and use this port address in local host this you will not get the message response.
# so we have to address our local port to 8000 port address , see the below command
docker run -it -p 8000:8000 youtube-nodejs
# -p means port and 8000:8000 means local port and container port
# Now you can access your application in your local host using this url http://localhost:8000
# To stop the container you can use this command
docker stop <container id>
# To remove the container you can use this command
docker rm <container id>
# To remove the image you can use this command
docker rmi <image id>
# to see the folder structure we need to use this below command 
# docker exec -it <container id> bash
docker exec -it 5f831e50e32f77e428530d9 bash

# Than use the ls command, you will se the folder structure
# To see the environment variable we can use this command
docker exec -it 5f831e50e32f77e428530d9 env
# If you want to change the port number manually and check the new port number is it running or not thn we use this command
docker run -it -e PORT=4000 -p 4000:4000 youtube-nodejs
# To push the code in you docker hub repository account then you below command 
docker login
docker build -t sanjeebskn/youtube-nodejs .
docker push sanjeebskn/youtube-nodejs


# docker composing concept
# docker-compose.yml file is used to define and run multi-container Docker applications.
# The file is written in YAML and defines the services, networks, and volumes for the application.
# To create a docker-compose.yml file, you can use the following command
 docker-compose up -d --build or docker compose up
 # -d means detached mode and --build means build the image before run the container
 # To stop the container you can use this command
 docker compose stop or docker compose down






