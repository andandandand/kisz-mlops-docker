# MLOps Docker for Beginners

# Installation Guide

## Introduction

Thank you for your interest in our workshop about deploying machine learning models using Docker. This guide provides instructions for installing and setting up all the tools and environments required to prepare for the workshop.
## Prerequisites
- A Python IDE of your choice.
- A package manager we will be using pip for the workshop.

## Installation Guide

### Step 1: Install Docker

#### For Windows/Mac:
- Visit the [Docker Desktop download page](https://www.docker.com/products/docker-desktop).
- Follow the installation instructions:
  - [Windows](https://docs.docker.com/desktop/windows/install/)
  - [Mac](https://docs.docker.com/desktop/mac/install/)

#### For Linux:
- Choose your Linux distribution and follow the installation guide:
  - [Ubuntu](https://docs.docker.com/desktop/install/ubuntu/)
  - [Fedora](https://docs.docker.com/desktop/install/fedora/)
  - [Debian](https://docs.docker.com/desktop/install/debian/)
#### Create a Docker Account:
- Create a Docker Account to be able to use all the features of Docker: [Docker signup page](https://hub.docker.com/signup)
- Open Docker Desktop and login to your account.
### Step 2: Install Git

- Download and install Git from the [official site](https://git-scm.com/).
- Validate the installation in the terminal:
  ```
  git --version
  ```

# Workshop Hands-On
## Hands-On 1: Hello-World toy example
1. (Optional) Look for the ```hello-world``` Docker image on Docker hub: https://hub.docker.com/
2. Download the Docker image using the command: ```docker pull hello-world```
3. List your Docker images with the command: ```docker image ls```
4. Create a container using the ```hello-world``` image by running: ```docker run hello-world```
5. List your Docker containers using: ```docker ps --all```
6. Remove your Docker container with the command: ```docker rm [ID]```
7. Create a self-deleting container with the ```hello-world``` image using: ```docker run --rm hello-world```

## Hands-On 2: Running Jupyter with Docker
1. Download the image: ```docker pull jupyter/base-notebook```
2. Start a self-deleting container using the command: ```docker run --rm jupyter/base-notebook```
3. Read the terminal output can you access it?
5. Forward the port ```8888``` from the Docker container to the host machine: ```docker run -p 8888:8888 --rm jupyter/base-notebook```

## Hands-On 3: Bind Mount
**Problem:** The container cannot access our file on our host machine. 

**Solution:** Use a bind mount to access our **model** directory inside the Jupyter Notebook.

**Task:** Complete the following command: ```docker run […] -p 8888:8888 --rm jupyter/base-notebook```

1. Read Docker Documentation: https://docs.docker.com/storage/bind-mounts/
2. **Hint:**  Mount the **model** source folder from the clone of the workshop code to the ```/home/jovyan/work``` target folder in the Docker container.

## Hands-On 4: FastAPI
**Task:** Fill out the **TODOs** in the ```app/api.py``` file
1. Read the FastAPI documentation: https://fastapi.tiangolo.com/tutorial/response-model/#response_model-parameter
2. Read about the request body: https://fastapi.tiangolo.com/tutorial/body/


## Hands-On 5: Dockerfile
1. Create a file with the name **Dockerfile**
2. Find **Python version 3.11** on [Docker Hub](https://hub.docker.com/) and use it as a Base Image: ```FROM your-base-image:1.0```
3. Change the working directory inside of the container: ```WORKDIR /app```
4. Copy the ```requirements.txt``` file from the host file system into the docker container: ```COPY requirements.txt /to-container/```
5. Run a pip install for all the packages required: ```RUN pip install -r requirements.txt```
6. Copy the rest of the application into the container: ```COPY /from-host/ /to-container/```
7. Start the uvicorn server through the terminal command: ```CMD uvicorn app.location:api_name --host 0.0.0.0```

## Live-Demo: Deploying the Container with Docker Compose
1. Build and run the Docker container with Docker Compose: ```docker compose up --build```
2. **Problem:** Container shuts down when terminal closes. **Solution:** ```docker compose up -d```
3. **Problem:** Container doesn't restart when machine restarts. **Solution:** Add ```restart:always``` to the ```compose.yaml``` file.
4. **Problem:** Application has errors and I need to see the logs. **Solution:** Use ```docker ps``` to get the container ID and then use  ```docker logs [ID]``` to read the logs.
5. Close the container using  ```docker compose down```
