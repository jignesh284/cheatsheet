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
- docker inspect [CONTAINER_NAME]

//Container logs from container running in detached mode
- docker logs [CONATINER_NAME]
                                
                                
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

# Creating Custom Image

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

//docker build-steps(layers) are cached if it fails on certain layer it returns from that particular layer onwards

// CMD VS ENTRYPOINT

1. CMD defines the command to exectute within the container when it start's
2. CMD can be defined as CDM followed by agruments array where the first element of the array is an executable command. 
- CMD ["command", "params"] example CMD ["sleep", "5"],  CMD ["nginx"] ,  CMD ["bash"]

3. ENTRYPOINT is similar to CMD it the only difference is it can append the agruments from the docker run command to ENTRYPOINT where as in case of CDM the commandline parameters override the CMD parameters completely
- ENTRYPOINT ["sleep"]
- docker run ubuntu-sleeper 10
+ Command executed on start will be "sleep 10" 

4. other way is to use both EntryPoint and CMD
- ENTRYPOINT ["sleep"]
- CMD ["10"] //in case the user povide argument from docker run it will override the CMD.
```

# Docker Networking
```diff
1. Docker creates 3 networks by default - "bridge", "none", "host"
2. Bridge is the default network a docker container attaches to
//Default network is "bridge network"
- docker run ubuntu
3. To specify a network for a container 
- docker run ubuntu --network=none
- docker run ubuntu --network=host
     
4. Bridge is a private internal network created by host. 
5. All the conatiners attached to Bridge get an internal ip address in series: 172.*
6. Containers can access each other using internal ip if required.
7. To access any container from outside we need to map [HOST_PORT]:[DOCKER_CONTAINER_PORT] 
  
8. Host network siginifies that all the PORTS from all containers get mapped by default to HOST PORT
9. This imply that we cannnot run two diffrent containers on same port as both will try and access the same port on host.
 
10. None network siginfies that the container is not connected to host or othere conatiners i.e it runs in isolation
 
11. By default docker creates just one bridge network. But we can create more the one bridge networks
- docker network create --driver network --subnet 182.18.0.0/16 custom-isolation-network
     
//list all the nwtwork
- docker network ls
     
//to ckeck the network specific details run
- docker inspect [CONT_NAME]
     
12. EMBEDDED DNS (container can communicate internally using CONT_NAME instead of ip) DNS always runs on 127.0.0.11
- mysql.connect( [CONT_NAME] )
```

# Docker Storage
```diff
1. create volume used to persist data from container on host 
- docker volume create save-data
//map the containers folder to the host folder
- docker run -v save-data:/var/lib/mysql [IMAGE_NAME]
    
//Alternative
- docket run --mount type=bind, source=/data/mysql, target=/var/lib/mysql mysql

```

# Docker Compose
```diff
1. If we need to run multiple containers for application we can create a docker-compose.yml file to do so.
  example: docker-compese.yml
      
    service:
        web:
            image: "python-flask"
        database:
            image: "mongos-db"
        messaging: 
            image: "redis:alpine"
        orchestration:
            image: "ansible"
         
2. to run the docker compose to build all conatiners use
- docker-compose up 

Another example of compose of docker-compose.yml
version: 2
services:
  redis:
    image: redis
    networks:
        back-end:

  dB:
    image: postgress:9.4
    networks:
        back-end:
        
  vote:
    build: ./vote            // can be used to build an image from Dockerfile
    //image: voting-app
    ports:
      - 5000: 80
    links:
      - redis
     networks:
        back-end:
        front-end:

  result:
    image: result-app
    ports:
      - 5001: 80
    links:
      - db
     networks:
        back-end:
        front-end:

  worker:
    image: result-app
    links:
      - db
      - redis
     networks:
        back-end:
      
   networks:
     front-end:
     back-end:
```


Thanks ♥️ :hearts: [Reference](https://www.youtube.com/watch?v=fqMOX6JJhGo)
