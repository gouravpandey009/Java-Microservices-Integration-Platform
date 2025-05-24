# Microservices Integrating Platform using Java

Demo Project Video 

<a href="https://dzone.com/articles/bootstrapping-a-microservice-architecturescreencas" target="_blank"><img src="http://img.youtube.com/vi/6LPDbgf5ssU/0.jpg" 
alt="Bootstrapping a microservice architecture" width="240" height="180" border="10" /></a>

Read about the project [here](https://dzone.com/articles/bootstrapping-microservices-your-microservice-arch)

Hey there! 👋

This project is like a starter kit for building cool microservices using Java. 🎒✨

We know starting with microservices can be super confusing, so we made this to help you out! 🧠💡

It's like giving you a ready-made playground where all the boring setup is already done — so you can just jump in and start playing! 🛝👨‍💻

If you're someone who wants to learn about microservices or maybe even use them for a real job, this is just for you! 🎯

So go ahead, explore it, change it, break it, fix it — and have fun while learning! 🚀🧩

🧠 Microservice Superpowers (Principles)
These are the awesome things microservices can do:

Grow big easily (Scalability) – Like LEGO bricks, just add more when you need!

Always ready (Availability) – Tries its best to never sleep or break.

Tough cookie (Resiliency) – Even if one part breaks, the rest keep going! 💪

Works alone (Independent, autonomous) – Each piece does its job all by itself.

No bossy boss (Decentralized governance) – Every part chooses its own tools and rules.

Oops-proof (Failure isolation) – If one part goes kaboom 💥, others are safe.

Auto-magic setup (Auto-Provisioning) – New parts can join the game all by themselves!

Fast and forever updates (Continuous delivery through DevOps) – Like getting new toys without stopping the game! 🎮🔧

🔧 Microservice Magic Tricks (Patterns)
These are the cool tricks microservices use to stay smart:

Circuit Breakers – Like a superhero shield 🛡️ that blocks too many bad calls.

API Gateway – A friendly gatekeeper that tells messages where to go.

CQRS (Command Query Responsibility Segregation) – One side talks, the other listens. No mix-ups! 📢👂

Saga Pattern – A story where each part takes turns doing its bit.

Event Sourcing – Keeps track of everything that happened, like a diary 📖.

Log Aggregation – All logs come together to party in one place 🥳.

Health Check – A quick “Hey, you okay?” to make sure everyone’s fine.

Service Discovery – Services play hide and seek, and still find each other! 👀

External Configuration – Settings kept outside so you can change them anytime.

Distributed Authentication – Everyone checks who you are, like getting a ticket at every ride in a fun park 🎟️🎢.


🛠️ Cool Toys You’ll See in This System (Technologies)
This project uses a bunch of awesome tech tools — each with a special job, like superheroes on a mission! 🦸‍♂️🦸‍♀️

Spring Boot – The main boss that brings everything together, super fast! ⚡

Spring Data – Helps you find, save, and play with your data easily. 📦🔍

Spring Cloud Eureka – Like a map 🗺️ so all your services can find each other.

Ribbon – Makes sure traffic is split fairly so nobody gets too tired. 🚦

Feign – Sends messages between services, like walkie-talkies! 📞

Hystrix – A smart safety switch that stops trouble before it spreads! 🚫🔥

Spring Admin – A control room to keep an eye on everything. 🎛️

📣 Talking & Watching Tools
ElasticSearch + Logstash + Kibana (ELK) – Like super glasses 🕶️ to watch and search through all the logs.

Nginx – A gatekeeper that handles who goes where! 🧍‍♂️➡️🚪

Docker Compose – A toy organizer that puts all pieces in place 🧸📦

JMX Monitoring – A health checker for the whole system. 🩺

Spring Security OAuth + JWT – Only lets in people with the right secret badge! 🕵️‍♂️🔐

💡 Magic & Messaging
Aspect-Oriented Programming (AOP) – Adds extra magic ✨ without messing with the core code.

Kafka + Spring Stream – Like a message bus that carries notes everywhere 🚌📨

Maven Multi-Module – Splits big things into smaller ones for easy peasy work. 🧩

Event Sourcing – Writes down every tiny thing that happens like a journal 📔

CQRS – Talks and listens happen in separate rooms, no shouting over each other! 🗣️👂

REST & WebSockets – Ways to chat — either politely or super fast and live! 🧑‍💻💬⚡

Jenkins – Your smart robot friend 🤖 that builds and sends updates all by itself!

And guess what? It’s all built using Java 8 – a powerful language that’s both cool and clever! ☕💻


![Alt text](assets/microservices-arch.jpg?raw=true "microservices architecture")


## How to use

* run `package-projects.sh`
* run `docker-orchestrate.sh`
* `docker-compose -p todo up` 

## Continuous deploy using Jenkins Pipeline
We have created a docker image in order to have continuous deploy in our project [here](https://github.com/apssouza22/build-deploy).

This image will contain all necessary to build our project, create the Docker images and 
deploy on AWS using ECS containers. 

### Deploy on AWS 
* Create your credentials on AWS 
* Create your cluster on AWS console
* Have the build-deploy container running (Checkout in the project's README how to do it)
* Access Jenkins painal
* Create a pipeline job
* Run the Job

### Accessing the services
* Authenticate -> ```curl -X POST -vu todo-app:123456 http://localhost:8017/oauth/token -H "Accept: application/json" -d "password=1234&username=apssouza22@gmail.com&grant_type=password&scope=write&client_secret=123456&client_id=todo-app"```   

* Get data using the access_token -> `localhost:8018/accounts?access_token={access_token}` or `curl -H "Authorization: Bearer $TOKEN" "localhost:8018/path"`

### Scaling 
NGINX will  be configured for browser caching of the static content and Load balance. For that we will need to scale our App Gateway 
and update manually the ports in `default.conf` file, in the upstream configuration section:

```
upstream backend {
  server gateway:8018;
  server gateway:DYNAMICPORT;
  server gateway:DYNAMICPORT;
}
```

And we will run the compose file with `--scale` parameter:

`docker-compose -f proxy-docker-compose.yml -p todo up --scale gateway=2`

### URLs
Monitoring stream - http://localhost:8022/turbine.stream

To-dos http://localhost:8015/todos

Users http://localhost:8016/accounts 

Eureka server - http://localhost:8010/

Config server - http://localhost:8888/

Boot admin - http://localhost:8026

Kimbana - http://localhost:5601

Elasticsearch Info: http://localhost:9200

Elasticsearch Status: http://localhost:9200/_status?pretty

NGINX Status: localhost:8055/nginx_status

docker-compose -p todo up
docker-compose -p todo down

## OBS
* In order to make ELK work we need to reserve 3GB RAM to docker(docker settings - advanced - memory )
* Have a look at the Readme of each service/ module to see the explanation about it.
* On Kimbana create a filter called `filebeat-*` to see the logs

## Useful Commands

### Creating to-do via Curl
```
curl -d '{"userEmail":"alex@test.com", "caption":"post caption", "description":"desc", "priority": 1}' -H "Content-Type: application/json" -X POST http://localhost:8015/todos
```

### Stopping, Starting, Restarting...

```
# running separated container and link to the network infrastructure
docker run -d -p 8018:8018  --network todo_net --add-host eureka:172.19.0.5 --add-host config:172.19.0.2 todo/reminder-service

# orchestrate start-up of containers, tailing the logs...
docker-compose -p music up -d container-name && docker logs elk --follow # ^C to break

# stopping containers
docker-compose todo stop
docker-compose todo down

# starting containers
docker-compose -p todo up

# removing containers
docker-compose todo rm

```

### Application Startup Issues

```bash
# stop / start Tomcat
docker exec -it container-name sh /usr/local/tomcat/bin/startup.sh
docker exec -it container-name sh /usr/local/tomcat/bin/shutdown.sh

# check logs for start-up issues...
docker exec -it container-name cat /usr/local/tomcat/logs/catalina.out
docker logs container-name
```

### Kafka
Inside the Kafka container

```
# event consume
/opt/kafka/bin/kafka-console-consumer.sh --zookeeper zookeeper:2181 --topic todo-mail --from-beginning

# producer console
/opt/kafka/bin/kafka-console-producer.sh --broker-list kafka:9092 --topic todo-mail

# Listing topics
/opt/kafka/bin/kafka-topics.sh --list --zookeeper zookeeper:2181

# Create topic
/opt/kafka/bin/kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic pcs
```

### Data
```
#create a new To-Do 
curl -H "Content-Type: application/json" -X POST -d '{"id":161,"caption":"Test caption 3","userEmail":"pandeygourav09@gmail.com","description":"description 3","createdat":null,"priority":2,"status":"PENDING","version":0,"valid":true}' http://localhost:8015/todos
```

## TODO
* Add private maven repository Artifactory
* Manager services integration through Spring Webflow
* Add Distributed Tracing



