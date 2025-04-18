# What is Docker Compose ?


Docker Compose is a powerful tool that simplifies the management of multi-container Docker applications. 

It allows developers and DevOps engineers to define, configure, and run multiple services using a single YAML file.

Instead of managing individual docker run commands, you can use a docker-compose.yml file to configure and start your entire application stack with a single command.


# Why Use Docker Compose ?


Simplifies Multi-Container Applications :-  Manage multiple services using a single file.

Improves Development Workflow :-  Easily set up and tear down environments.

Supports Networking and Dependencies :-  Automatically links services together.

Compatible with Different Environments :-  Use the same configuration for local development and production.


# Components of compose file


version - specifies the version of the Compose file.

services - it the services in your application.

networks - you can define the networking set-up of your application.

volumes - you can define the volumes used by your application.

configs - configs lets you add external configuration to your containers. Keeping configurations external will make your containers more generic.


# Installing Docker Compose

```
sudo yum update -y
sudo yum install -y docker
sudo service docker start
sudo systemctl enable docker
sudo yum install -y python

sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo yum install -y libxcrypt
ls /lib64/libcrypt.so.1
docker-compose --version
```

OR

```
sudo apt update
sudo apt install docker.io -y
sudo apt install docker-compose -y
```

### Docker-compose file concept :-

Example of docker-compose file


Lets write the basic compose file to understand how it works

Create a file with docker-compose.yaml name

```
version: "3"
services:
  webapp1:
    container_name: container_name
    build: <your-Dockerfile-Path>
    ports:
      - "host_port:container_port"

  webapp2:
    container_name: container_name
    build: <your-Dockerfile-Path>
    ports:
      - "host_port:container_port"

```

In the above compose file, i am creating 2 services (webapp1, webapp2). 

For each service we have to provide container_name, path of your Dockerfile and ports to access the application.



## LAB-1 : compose file to create multiple services

```
git clone https://github.com/icloudrepo1/web-compose.git
```

```
cd web-compose
```

```
vi docker-compose.yml
```


```
---
version: "3"
services:
  movie:
    container_name: movie-container
    build: ./movie-tickets
    ports:
      - "8081:80"

  bus:
    container_name: bus-container
    build: ./bus-tickets
    ports:
      - "8082:80"

  train:
    container_name: train-container
    build: ./train-tickets
    ports:
      - "8083:80"

```


lets build the Dockerfiles

```
docker-compose build
```

To create the services

```
docker-compose up -d
```

Lets check the containers(services)

```
docker-compose ps
```


(lets check the output for 3 services)

### Method-1 :- docker-compose.yml for Scaling with Custom Port Numbers(Manual scaling)

Since you’re giving each service a different name and port, Docker Compose treats them as independent containers and avoids the port conflict issue that happens when scaling with --scale.

```
version: "3"
services:
  movie1:
    build: ./movie-tickets
    ports:
      - "8072:80"
    environment:
      - MOVIE_SERVICE=movie

  movie2:
    build: ./movie-tickets
    ports:
      - "8073:80"
    environment:
      - MOVIE_SERVICE=movie

  movie3:
    build: ./movie-tickets
    ports:
      - "8074:80"
    environment:
      - MOVIE_SERVICE=movie

  movie4:
    build: ./movie-tickets
    ports:
      - "8075:80"
    environment:
      - MOVIE_SERVICE=movie

  bus:
    container_name: bus-container
    build: ./bus-tickets
    ports:
      - "8082:80"

  train:
    container_name: train-container
    build: ./train-tickets
    ports:
      - "8083:80"

```

```
docker-compose down
docker-compose up -d
```


### Method-2 :-


Docker Compose doesn’t support port mapping per replica, and it doesn’t scale like Docker Swarm does with internal load balancing.

if suppose `docker-compose up --scale <service_name>=<number_of_replicas>` then, Port conflicts

( If your service exposes a port (e.g. ports: - "8072:80"), Compose cannot bind the same port for each replica, so scaling will fail unless, You remove the ports )

```
version: '3'
services:
  movie:
    build: ./movie-tickets
    expose:
      - "80"  # Use 'expose' instead of 'ports'
    environment:
      - MOVIE_SERVICE=movie
  bus:
    container_name: bus-container
    build: ./bus-tickets
    ports:
      - "8082:80"

  train:
    container_name: train-container
    build: ./train-tickets
    ports:
      - "8083:80"
```

```
docker-compose up --scale movie=4
```

## LAB-2 : Volumes in Compose File

In the above example we just used containers and images on our compose file, now lets use volumes for our compose file

```
docker-compose down
```

```
vi docker-compose.yml
```

```
---
version: "3"
services:
  movie:
    container_name: movie-container
    build: ./movie-tickets
    ports:
      - "8081:80"
    volumes:
      - movie_volume:/usr/share/nginx/html:ro

  bus:
    container_name: bus-container
    build: ./bus-tickets
    ports:
      - "8082:80"
    volumes:
      - bus_volume:/usr/share/nginx/html:ro

  train:
    container_name: train-container
    build: ./train-tickets
    ports:
      - "8083:80"
    volumes:
      - train_volume:/usr/share/nginx/html:ro

volumes:
  movie_volume:
  bus_volume:
  train_volume:

```

lets build the Dockerfiles

```
docker-compose build
```

Now lets use docker-compose up -d command to create a docker containers, so the containers will recreate with volumes

```
docker-compose up -d
```

Now lets check the containers and volumes

```
docker-compose ps
```

```
docker volume ls
```


Now if you make any changes in volume it will replicated in the output. So lets change the code on docker volumes.

in Movie Tickets :- i have Hollywood movie like avengers, now i am changing to Tollywood movies like RRR, PUSHPA & KGF


```
vim /var/lib/docker/volumes/paytm_movie_volume/_data/index.html
```

(change code ----  I have modified the code on volumes, now we can see the changes on production.)



## LAB-3 : Networks in Compose File


When we execute the compose file, it will create a network by default for our services.But if you wish to restrict the connection between the services we have to maintain each network for each services individually.


```
vi docker-compose.yml
```

```
---
version: "3"
services:
  movie:
    container_name: movie-container
    build: ./movie-tickets
    ports:
      - "8081:80"
    volumes:
      - movie_volume:/usr/share/nginx/html:ro
    networks:
      - movie_network

  bus:
    container_name: bus-container
    build: ./bus-tickets
    ports:
      - "8082:80"
    volumes:
      - bus_volume:/usr/share/nginx/html:ro
    networks:
      - bus_network

  train:
    container_name: train-container
    build: ./train-tickets
    ports:
      - "8083:80"
    volumes:
      - train_volume:/usr/share/nginx/html:ro
    networks:
      - train_network

#declare the volumes that you want to create here        
volumes:
  movie_volume:
  bus_volume:
  train_volume:

#declare the networks that you want to create here
networks:
  movie_network:
    driver: bridge
  bus_network:
    driver: bridge
  train_network:
    driver: bridge

```

lets build the Dockerfiles

```
docker-compose build
```

Lets use docker-compose up -d command to recreate the containers with their own networks.

By using the above command, old containers will gets deleted and new containers will be created with networks.

```
docker-compose up -d
```

lets check the networks

```
docker network ls
```

(you can inspect each container to check the networking configurations.)



## LAB-4 : ENV values in Compose File


---not completed---
