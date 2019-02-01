# Docker commands
__Docker Version :__  
    `docker version`  
    
__Information of Docker container and images in your docker :__  
    `docker info`  
    
__Cloning Image from [Docker Hub](https://hub.docker.com/_/tomcat) :__   
    `docker image pull {image_name:veriosn}`
- For cloning tomcat:8.0 image in your docker `docker image pull tomcat:8.0`

__For listing all images in your docker :__  
    `docker image ls` 

__For removing Image from Docker :__
    `docker image rm {image_name}`
    `docker image rm {image_id}`  
    
__Creating Docker Container :__  
    `docker container create --publish {image_file_expose_port:local_machine_port} --name {container_name}`
- For creating tomcat container in your docker `docker container create --publish 8082:8080 --name my-tomcat-container tomcat:8.0`

__For listing all container in your docker :__  
    `docker container ls`
    `docker container ls -a` 
    `docker container ps`   
    
__For starting container in your docker :__  
    `docker container start -it {container_name}` for interactive mode 
    `docker container start -it {container_id}`
    `docker container start -d {container_name}` for detach mode (running in background)  
    
__For executing bash command inside your docker container :__  
    `docker contianer exec -it {container_name} bash`  
- `docker container exec -it my-tomcat-container bash`   it will list your docker tomcat container your docker as `:/usr/local/tomcat `   

__For stoping container in your docker :__  
    `docker container stop {container_name}`  
    `docker container stop {container_id}`  

__For removing container in your docker :__  
    `docker container rm {container_name}`  
    `docker container rm {container_id}`
    `docker container rm -f {container_name}` for force remove container while it is still in process/running  
    
__For removing multiple container in your docker :__  
    `docker container rm {container_id} {container_id}`  
  
__Creating image file for your application :__  
    Following code is for creating image file for war which will be deploy in docker tomcat container.  
    Create a file with name Dockerfile in root directory of your application without any extension and add following lines in it.  
```sh
# We are extending everything from tomcat:8.0 image ...

FROM tomcat:8.0

MAINTAINER {your_name}  

# COPY {path-to-your-application-war} {path-to-webapps-in-docker-tomcat}  

COPY some-app/target/some-app.war /usr/local/tomcat/webapps/
```   
    
`docker image build -t {your_name/image_name} ./`  
- `docker image build -t your_name/some-app-image ./`  
Now if you list images in your docker `docker image ls -a` it will contain image that you have just created for your application.  

__For deploying application image in your docker :__    
`docker container run -it --publish 8081:8080 your_name/some-app-image` Your application will be running in docker container.
