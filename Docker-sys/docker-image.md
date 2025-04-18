# Docker Images

A Docker image is a lightweight, standalone, and executable package that contains everything needed to run a piece of software. 

It includes the code, runtime, libraries, environment variables, and dependencies required to run an application. 

An image is a read-only template with instructions for creating a Docker container. 

Often, an image is based on another image, with some additional customization. 

For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your own images or you might only use those created by others and published in a registry. 

To build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. 

Each instruction in a Dockerfile creates a layer in the image. 

When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.



### Key Points :-

Docker images are immutable (unchangeable after creation).

Docker images are built using a Dockerfile, which defines the steps to create the image.

Images can be stored in Docker registries, such as Docker Hub, where you can push and pull images.

Once an image is built, it can be run as a container. Containers are instances of images that can be started, stopped, and moved between different environments (like local development, testing, or production).

In simple terms, think of a Docker image as a blueprint for creating a Docker container.


### Creating a Docker Image using DOCKER FILE

To create a Docker image, you'll need a Dockerfile. This file contains instructions on how to build the image. 

Writing a Dockerfile is a straightforward process that involves defining a series of instructions that Docker uses to build an image. 


### Basic Structure of a Dockerfile


##### FROM : Specifies the base image for your Docker image (the starting point).

##### RUN : Executes commands inside the container during the image build process.

##### COPY : Copies files from your local machine into the container.

##### ADD : Similar to COPY, but with extra capabilities (e.g., can extract tar files).

##### WORKDIR : Sets the working directory inside the container.

##### CMD : Specifies the default command to run when a container starts from the image.

##### ENTRYPOINT : Similar to CMD but allows for overriding with command-line arguments.

##### EXPOSE : Defines the port number the container will listen on.

##### ENV : Sets environment variables.

##### VOLUME : Creates a mount point for a volume (shared data between containers or the host).

##### USER : Specifies the user to run commands as inside the container.



### LAB-1 :- Example Dockerfile for a HTML/CSS Web App


#### STEP-1 : Create Project Folder

```
mkdir my-webapp
cd my-webapp
```


#### STEP-2 : Create the index.html file to represent your homepage


vi index.html


```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>my-WebApp</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Welcome to Docker World!</h1>
    <p> Devops Devops.</p>
</body>
</html>
```

#### STEP-3 : Create a styles.css file to style the webpage 


vi styles.css


```
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    text-align: center;
    padding-top: 50px;
}

h1 {
    color: #2a9d8f;
}

p {
    color: #264653;
}
```


#### STEP-4 : You need a Dockerfile to package your HTML and CSS files into a Docker image  


vi Dockerfile


```
# Use the official Nginx image from the Docker Hub as the base image
FROM nginx:alpine

# Remove the default Nginx welcome page
RUN rm -rf /usr/share/nginx/html/*

# Copy the current directory contents into the Nginx container
COPY . /usr/share/nginx/html

# Expose port 80 to make the app accessible on this port
EXPOSE 80

# The Nginx server will start by default, no need to specify a CMD
```


Explanation of the Dockerfile :-


FROM nginx:alpine :- This uses the official Nginx image based on the lightweight Alpine Linux distribution.

RUN rm -rf /usr/share/nginx/html/ :- Removes the default Nginx content to replace it with your own files.

COPY . /usr/share/nginx/html :- Copies all the files (your index.html and styles.css) from the current directory on your machine into the container’s Nginx HTML directory.

EXPOSE 80 :- Exposes port 80 so the container can serve your web app on that port.



#### STEP-5 : Now that you’ve created the Dockerfile, you can build the Docker image


```
docker build -t my-webapp-img .
```

-t my-webapp-img :- This tags the image with the name my-webapp-img.

. :- Refers to the current directory, which contains the Dockerfile.


#### STEP-6 : Push the Image to Docker Hub


Tag the image for Docker Hub

```
docker tag my-webapp-img yourdockerhubusername/my-webapp-img:V1
```


Log in to Docker Hub

```
docker login
```

Push the image

```
docker push yourdockerhubusername/my-webapp-img:V1
```

#### N.B. = Run the Docker Container

```
docker run -d -p 8080:80 --name webapp-container-1 my-webapp-img
```


-d :- Runs the container in detached mode (in the background).

-p 8080:80 :- Maps port 8080 on your host machine to port 80 on the container (the default HTTP port).

--name webapp-container-1 :- Names the container webapp-container-1.

my-webapp-img :- The image you built earlier.




(Open your web browser and Access it)


================END================================
