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

//running tags
- docker run redis:4.0  //specifing version of the service will check the tags on dockerhup and download the image with that tag

//running -stdin
//-i means intractive mode where the terminal waits for user input
//-t sudo terminal which attaches containers sudo terminal
- docker run -it [IMAGE_NAME]  

//running -PORT mapping (maps the host port to container port)
- docker run -p [HOST_PORT]:[CONTAINER_PORT] [IMAGE_NAME] 

//running VOLUME mapping (host directory to container directory)
- docker run -v [HOST_PATH]:[CONTAINER_PATH] [IMAGE_NAME] example: docker run -v /opt/datadir:/var/lib/mysql mysql

//running container with Environment Variables
- docker run -e [VARIBALE_NAME]=[VALUE] [IMAGE_NAME]


//Inspect container (returns details of the container settings(Environment_varibales) in json format )
docker inspect [CONTAINER_NAME]

//Container logs from container running in detached mode
docker logs [CONATINER_NAME]
                                
                                
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

#Creating Custom Image

```diff
//Start by thinking how to deploy a flask application
1. OS - Ubuntu
2. Update apt repo
3. install dependencies using apt
4. install python dependencies using pip
5. copy source code to /opt folder 
6. run the web server using flask command

//docker files are instructions(FROM, RUN, COPY, RNTRYPOINT) and arguments(rest are agruments) format

create a file name it 'Dockerfile'
add following lines to it

//defines base of for the container (every docker is based on OS or other docker Image)  
//All docker file 'MUST' start with from statement
- FROM Ubuntu

//RUN command runs instructions on base Image
- RUN apt-get upddate
- RUN apt-get install python

- RUN pip install flask
- RUN pip install flask-mysql

//Copy instruction copy file from local system to docker_image
- COPY . /opt/source-code

//entry point specifies commad that will run when the dockerimage start as container
- ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run

//Build command (creates image locally)
- docker build Dockerfile -t [IMAGE_NAME]

//Docker push command (push it to Dockerhub)
- docker push [IMAGE_NAME]

//Layered Architecture: Dockerbuilds images in layered format to check
- docker history [IMAGE_NAME]

//docker build-steps(layers) are cached if it fails on certain layer it reruns from that particular layer onwards










```

Thanks ♥️ :hearts: [Reference](https://www.youtube.com/watch?v=fqMOX6JJhGo)
