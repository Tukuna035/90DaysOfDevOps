Day 29 – Introduction to Docker

Challenge Tasks
Task 1: What is Docker?
Research and write short notes on:
•	What is a container and why do we need them?
•	Containers vs Virtual Machines — what's the real difference?
•	What is the Docker architecture? (daemon, client, images, containers, registry)
Draw or describe the Docker architecture in your own words.

What is Docker?
Docker is an open-source platform used to build, package, and run applications inside containers.
In simple words:
👉 Docker helps you run your application the same way on your laptop, test server, and production server — without “it works on my machine” problems.
Docker was created by Docker, Inc. in 2013.
________________________________________
🐳 What is a Container?
A container is a lightweight package that includes:
•	Application code
•	Runtime (Java, Python, Node, etc.)
•	Libraries
•	Dependencies
•	System tools
Everything needed to run the app.
Containers share the host OS kernel, so they are:
•	Lightweight
•	Fast
•	Portable
________________________________________
🔹 Why Docker is Important?
Before Docker:
•	Apps were installed directly on servers
•	Dependency conflicts happened
•	Different environments caused failures
With Docker:
•	Consistent environments
•	Easy deployment
•	Better scalability
•	Faster CI/CD pipelines
________________________________________
🔹 Docker vs Virtual Machine
Docker (Container)	Virtual Machine
Lightweight	Heavy
Shares host OS	Has full OS
Starts in seconds	Takes minutes
Uses less RAM	Uses more RAM
________________________________________
🔹 Core Docker Components
1.	Docker Engine – Runs containers
2.	Docker Image – Blueprint/template for containers
3.	Docker Container – Running instance of image
4.	Dockerfile – File to build Docker image
5.	Docker Hub – Public image registry
Official public registry: Docker Hub
________________________________________
🔹 Basic Docker Workflow
# Build image
docker build -t myapp .

# Run container
docker run -p 8080:80 myapp
________________________________________
🔹 Real Example (DevOps Perspective)
As someone learning DevOps, Docker helps you:
•	Package your application
•	Deploy to Kubernetes
•	Use in CI/CD pipelines
•	Ensure environment consistency
Example:
•	Developer builds image
•	Pushes to Docker Hub
•	Production server pulls and runs it
________________________________________
🔥 One-Line Definition (Interview Ready)
Docker is a containerization platform that packages applications and their dependencies into lightweight, portable containers for consistent deployment across environments.
________________________________________

Docker Architecture

🐳 Docker Architecture
Docker architecture follows a client-server model.
It mainly has 3 major components:
1.	Docker Client
2.	Docker Host (Docker Engine)
3.	Docker Registry
Docker was developed by Docker, Inc.
________________________________________
🔹 1️⃣ Docker Client
This is what you use when you run commands like:
docker build
docker run
docker pull
•	The client sends requests to the Docker Daemon.
•	Communication happens via:
o	REST API
o	Unix socket
o	TCP
👉 Example:
When you type docker run nginx, the client sends a request to the daemon.
________________________________________
🔹 2️⃣ Docker Host (Docker Engine)
The Docker Host contains:
✅ Docker Daemon (dockerd)
•	Core service
•	Builds images
•	Runs containers
•	Manages networks & volumes
✅ Docker Images
•	Read-only templates
•	Used to create containers
✅ Docker Containers
•	Running instances of images
•	Isolated processes
________________________________________
🔹 3️⃣ Docker Registry
A registry stores Docker images.
Default public registry:
Docker Hub
Other examples:
•	Private registry
•	Cloud registries (AWS ECR, Azure ACR, GCR)
When you run:
docker pull nginx
Docker pulls the image from Docker Hub (if not available locally).
________________________________________
🔄 How Docker Architecture Works (Step-by-Step)
Let’s say you run:
docker run nginx
Step 1:
Docker Client sends request to Docker Daemon.
Step 2:
Daemon checks if image exists locally.
Step 3:
If not found → pulls image from Docker Hub.
Step 4:
Creates container from image.
Step 5:
Runs container as an isolated process.
________________________________________
📊 Simple Architecture Diagram (Conceptual)
        +------------------+
        |   Docker Client  |
        +------------------+
                 |
                 v
        +------------------+
        |  Docker Daemon   |
        |  (Docker Engine) |
        +------------------+
           |      |      |
           v      v      v
        Images  Containers  Networks/Volumes
                 |
                 v
          Docker Registry
         (Docker Hub)
________________________________________
🔎 Internal Components (Important for Interviews)
•	containerd → Container runtime
•	runc → Low-level container runtime
•	Namespaces → Isolation
•	cgroups → Resource limits
•	Union File System → Image layers
________________________________________
🎯 Interview One-Line Answer
Docker architecture follows a client-server model where the Docker client communicates with the Docker daemon to build, run, and manage containers, while images are stored in registries like Do

Task 2: Install Docker
1.	Install Docker on your machine (or use a cloud instance)
2.	Verify the installation
3.	Run the hello-world container
4.	Read the output carefully — it explains what just happened


ubuntu@ip-172-31-18-163:~$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
17eec7bbc9d7: Pull complete
Digest: sha256:ef54e839ef541993b4e87f25e752f7cf4238fa55f017957c2eb44077083d7a6a
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/


Task 3: Run Real Containers
1.	Run an Nginx container and access it in your browser
2.	Run an Ubuntu container in interactive mode — explore it like a mini Linux machine
3.	List all running containers
4.	List all containers (including stopped ones)
5.	Stop and remove a container

ubuntu@ip-172-31-18-163:~$ docker run -d -p 8080:80 --name mynginx nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
0c8d55a45c0d: Pull complete
46bf3a120c8e: Pull complete
4f4efe02d542: Pull complete
7b6cb8ccac7b: Pull complete
f73400a233fd: Pull complete
47cd406a84ef: Pull complete
bae5a1799a80: Pull complete
Digest: sha256:341bf0f3ce6c5277d6002cf6e1fb0319fa4252add24ab6a0e262e0056d313208
Status: Downloaded newer image for nginx:latest
e7f81b82c3c149b128066359a805d76a2baa38f10d690ef60d695d5aea42b48e
ubuntu@ip-172-31-18-163:~$ docker run -itd --name myubuntu ubuntu
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
01d7766a2e4a: Pull complete
Digest: sha256:d1e2e92c075e5ca139d51a140fff46f84315c0fdce203eab2807c7e495eff4f9
Status: Downloaded newer image for ubuntu:latest
e7ebca7db51c0c411dbda338bf6d89e6a1bd2a50490012b44d79fe71625b11dd


ubuntu@ip-172-31-18-163:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                     NAMES
e7ebca7db51c   ubuntu    "/bin/bash"              20 seconds ago   Up 20 seconds                                             myubuntu
e7f81b82c3c1   nginx     "/docker-entrypoint.…"   54 minutes ago   Up 54 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   mynginx
ubuntu@ip-172-31-18-163:~$ docker exec -it e7ebca7db51c bash


Task 4: Explore
1.	Run a container in detached mode — what's different?
2.	Give a container a custom name
3.	Map a port from the container to your host
4.	Check logs of a running container
5.	Run a command inside a running container
Great 👍 let’s answer all 5 clearly with commands + explanation.
________________________________________
1️⃣ Run a container in detached mode — what’s different?
Command:
docker run -d nginx
What’s different?
•	-d = detached mode
•	Container runs in the background
•	Your terminal is free immediately
•	Logs are not shown automatically
Without -d:
docker run nginx
•	Runs in foreground
•	Terminal is attached to container output
•	You must stop it (Ctrl+C) to return to shell
👉 So detached mode = background execution.
________________________________________
2️⃣ Give a container a custom name
By default Docker gives random names like sleepy_brown.
To set your own name:
docker run -d --name my-nginx nginx
Now you can manage it easily:
docker stop my-nginx
docker logs my-nginx
docker rm my-nginx
Much better than using container ID.
________________________________________
3️⃣ Map a port from the container to your host
Example using Nginx (which runs on port 80 inside container):
docker run -d -p 8080:80 --name web nginx
Format:
-p HOST_PORT:CONTAINER_PORT
Meaning:
•	Host port → 8080
•	Container port → 80
Now open in browser:
http://localhost:8080
Without -p, the container service is not accessible from your system browser.
________________________________________
4️⃣ Check logs of a running container
docker logs web
To follow logs live:
docker logs -f web
Useful for:
•	Debugging
•	Checking startup errors
•	Monitoring application output
________________________________________
5️⃣ Run a command inside a running container
Use docker exec.
Open interactive shell:
docker exec -it web sh
(Use bash if available.)
Now you're inside the container.
Example commands:
ls
ps aux
cat /etc/nginx/nginx.conf
Exit:
exit
Run single command without entering shell:
docker exec web ls /
________________________________________
🚀 Quick Combined Example
docker run -d -p 8080:80 --name web nginx
docker ps
docker logs web
docker exec -it web sh
docker stop web
docker rm web

Hints
•	docker run, docker ps, docker stop, docker rm
•	Interactive mode: -it flag
•	Detached mode: -d flag
•	Port mapping: -p host:container
•	Naming: --name
•	Logs: docker logs
•	Exec into container: docker exec
Why This Matters for DevOps
•	Docker is the foundation of modern deployment. Every CI/CD pipeline, Kubernetes cluster, and microservice architecture starts with containers. Today you took the first step.



