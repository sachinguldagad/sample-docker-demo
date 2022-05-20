Eureka + Zuul + Sample Service + Docker
 
{If you want to skip this commands you have to write "docker-compose.yaml" file. 
 But first you have images already build on Docker othwerwise it will not run 
 To excecute this file:->Command: docker-composer up
 }

Commands to Execute Sample Project on Docker:

1. docker network create sample-nw
2. docker container run --name mysqldb -p 3300:3300 --network sample-nw -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=user_database   -d mysql:5.7
   [check mysqldb container is running. If mysqldb not running then close MySQL port from local system (windows seaarch -> services-> Mysql-> right click -> stop)]
3. docker image build -t eureka-service .
4. docker image build -t zuul-service .
5. docker image build -t sample-service .
6. docker container run --name eureka-service -p 8761:8761 --network sample-nw -d eureka-service
7. docker container run --name zuul-service -p 8762:8762 --network sample-nw -d zuul-service
8. docker container run --name sample-service -p 9730:9730 --network sample-nw -d sample-service

Troubleshoot:
1. When writing application.properties, please cheack where you writing "localhost" it should be replace by respective container name.
2. While creating .jar file skip the tests.[maven build... -> clean package -> after writing command you see "Skip Tests" checkbox -> tick it. ]
3. While accessing port on local system (browser) use "localhost" instead of container id.
