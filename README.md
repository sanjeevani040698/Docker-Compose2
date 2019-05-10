# Docker Compose UseCase
This is another example of docker-compose in which we link self made images together.

The yaml file looks something like this:

version: '2'                                                                                                                            
services:                                                                                                                           
  web1:                                                                                                               
   #build: ./Docker_main            # microservice is in the folder Docker_main of the current directory                                                                                                             
   image: image_main                                                                                                                    
   ports:                                                                                                                 
    - 5000:8080                                                                                                         
   #volumes:                                                                                                                              
    #- ./web_files:/usr/local/tomcat/webapps/webapp                                      
   volumes:                                                                                                                 
    - ./Docker_main:/usr/local/tomcat/folder                                                                                      
  web2:                                                                                                                             
    #build: ./Docker_result         # other dependent microservice is in the folder Docker_result of the current directory                                                             
    image: image_result                                                                                                     
    ports:                                                                                                                    
     - "5001:80"                                                                                                                                    
    depends_on:                                                                                                                   
     - web1                       
     
The two services described here, web1 and web2, can be considered as two microservices of a whole application that need to linked together.

We can build these services in the yaml file (by using build: ./folder) or put the image (as image: image_name) here.               
We can also build a particular service before running the dompose file by command: docker-compose build web1

Then we specify the mapping of host machine and container.

We can also volume mount the directories of the container using -volumes.                                                     
For example, in the service web1 the first mount is to facilitate live changes in the the web application.                      
The other one is to get a directory of the container reflected on the host machine.

Similarly, we can define as many services as required in the yaml file.

We use the 'depends_on: service_name' key-value pair for estabilishing dependencies of a service on the other, if any.
