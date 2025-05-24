```markdown
# 🚀 Java Microservices Integration Platform

A **starter kit** for building scalable, resilient, and modular microservices using **Java & Spring Boot**.

> 🎥 **Demo Video**  
[![Watch the Demo](http://img.youtube.com/vi/6LPDbgf5ssU/0.jpg)](https://dzone.com/articles/bootstrapping-a-microservice-architecturescreencas)

📖 Read the full article: [Bootstrapping Microservices](https://dzone.com/articles/bootstrapping-microservices-your-microservice-arch)

---

## 🌟 About the Project

Hey there! 👋  
This project is like your **microservices playground** — ready to use, experiment with, and learn from. Everything is pre-configured so you can **focus on building**, not setup.

Whether you're a curious learner or planning your production architecture — **this is your launchpad**. 🎯

---

## 🧠 Microservices Principles (Superpowers)

| Principle              | Description |
|------------------------|-------------|
| 🔁 **Scalability**         | Like LEGO blocks — add more pieces as needed |
| 💡 **Availability**        | Designed to stay online and responsive |
| 🛡️ **Resiliency**          | Fault-tolerant — one service fails, others keep going |
| 🤖 **Autonomy**            | Services work independently |
| 📦 **Decentralized Governance** | Services use their own tools/rules |
| 💥 **Failure Isolation**   | One crash doesn't break the system |
| ⚙️ **Auto-Provisioning**   | New services spin up automatically |
| 🔄 **Continuous Delivery** | Rapid, safe deployments via DevOps |

---

## 🔧 Common Microservice Patterns

- 🛡️ **Circuit Breaker** (Hystrix)
- 🚪 **API Gateway** (Nginx)
- 📢👂 **CQRS** (Separate write & read)
- 📖 **Event Sourcing**
- 🔄 **Saga Pattern**
- 📊 **Log Aggregation** (ELK)
- ❤️ **Health Checks**
- 🧭 **Service Discovery** (Eureka)
- 🧪 **External Configuration**
- 🔐 **Distributed Authentication**

---

## 🛠️ Technologies Used

| Category        | Tools & Frameworks |
|----------------|--------------------|
| ⚙️ Core Framework | Spring Boot, Maven Multi-Module |
| 🧠 Data Layer    | Spring Data JPA |
| 🌐 Communication | Feign, REST, WebSockets, Kafka |
| 🗺️ Discovery     | Spring Cloud Eureka |
| 🔄 Load Balancing | Ribbon |
| 🚧 Fault Tolerance | Hystrix |
| 🛡️ Security       | Spring Security, OAuth2, JWT |
| 🎛️ Admin & Ops   | Spring Admin, JMX Monitoring |
| 🔍 Observability | ELK Stack (ElasticSearch, Logstash, Kibana) |
| 🧪 Config & Gateway | Nginx, External Config |
| 🐳 Containerization | Docker Compose |
| 🤖 CI/CD         | Jenkins |

---

## 💬 Messaging & Advanced Features

- ✨ **Aspect-Oriented Programming (AOP)**
- 📖 **Event Sourcing**
- 🗣️👂 **CQRS (Command & Query Separation)**
- 📦 **Kafka with Spring Stream**
- ⚡ **Live communication with WebSockets**

---

## 🧩 Why Use This Platform?

✅ Jump-start microservice development  
✅ Clean modular architecture  
✅ Pre-configured tools & patterns  
✅ Ready for real-world use cases  
✅ Built with **Java 8** — modern and stable ☕

---

## 🏗️ Project Structure

```

/src
└── service-a
└── service-b
└── gateway
└── discovery
└── config-server
/docker-compose.yml
/pom.xml

````

---

## 📦 How to Run (Quick Start)

1. Clone the repo  
   ```bash
   git clone https://github.com/gouravpandey009/Java-Microservices-Integration-Platform.git
   cd Java-Microservices-Integration-Platform
````

2. Start services using Docker Compose

   ```bash
   docker-compose up --build
   ```

3. Access:

   * Gateway: `http://localhost:8080`
   * Eureka Dashboard: `http://localhost:8761`
   * Admin Panel: `http://localhost:8081`
---

> *“Build modular. Scale fast. Fail safe. Welcome to Microservices, the Java way.”* ☕


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



