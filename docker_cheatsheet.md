# Getting Started with docker 
[Test your knowlwedge once you learn all the commands](https://kodekloud.com/p/docker-labs)

```diff
Theory:

+ docker image  --- is like a class of java
+ docker container --- its like the instance of that class
+ docker conatier sleeps if no active process is running inside the container
+ if the code crash inside container the container will exit 
+ run attach containers runs in foreground . we cannot use terminal for other activities
+ run detach containers runs in backgound . we can use terminal for other process as terminal returns


//to start a docker container(default attach mode)
- docker run --name [name_for_container]  [IMAGE_NAME]

//to start a docker container in detached form
- docker run -d [IMAGE_NAME]

//get back to the attach mode in detached container
- docker attach [CONT_NAME/ID]


//list all running containers
- docker ps

//list all images on the machine
- docker images

// for all previously existed + currently running containers
- docker ps -a

//Stop container
- docker stop [CONT_NAME]

//Remove a stoped container permanently 
- docker rm [CONT_NAME]

//Remove a image from local machine (delete's local copy of image from device) when no containers are running on image
- docker rmi [IMAGE_NAME]

//To download the image locally
- docker pull [IMAGE_NAME]

//Execute a command inside docker container
- docker exec [IMAGE_NAME] [command]  example: docker exec [Name] cat /etc/host 

```
