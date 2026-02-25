Day 30 – Docker Images & Container Lifecycle

Challenge Tasks
Task 1: Docker Images
1.	Pull the nginx, ubuntu, and alpine images from Docker Hub
2.	List all images on your machine — note the sizes
3.	Compare ubuntu vs alpine — why is one much smaller?
4.	Inspect an image — what information can you see?
5.	Remove an image you no longer need
Great 👍 this is core Docker image practice. Let’s go step-by-step.
________________________________________
1️⃣ Pull the nginx, ubuntu, and alpine images from Docker Hub
docker pull nginx
docker pull ubuntu
docker pull alpine
This downloads images from Docker Hub to your local machine.
You can verify:
docker images
________________________________________
2️⃣ List all images on your machine — note the sizes
docker images
Example output (sizes may vary slightly):
REPOSITORY	TAG	SIZE
nginx	latest	~190MB
ubuntu	latest	~75MB
alpine	latest	~7MB
You’ll notice Alpine is extremely small.
________________________________________
3️⃣ Compare Ubuntu vs Alpine — why is one much smaller?
🟢 Ubuntu
•	Full Debian-based Linux distribution
•	Includes many utilities and libraries
•	Uses apt package manager
•	Larger base filesystem
🟢 Alpine
•	Minimal Linux distribution
•	Uses musl libc instead of glibc
•	Uses apk package manager
•	Very few preinstalled packages
That’s why:
Image	Approx Size	Why
ubuntu	~70–80MB	Full OS userspace
alpine	~5–10MB	Minimal + lightweight libc
Alpine is popular in production because:
•	Smaller image = faster pull
•	Smaller attack surface
•	Lower storage usage
But sometimes Ubuntu is needed if:
•	Your app depends on glibc
•	You need more debugging tools
________________________________________
4️⃣ Inspect an image — what information can you see?
Use:
docker inspect nginx
You’ll see a large JSON output containing:
•	Image ID
•	Created date
•	OS / Architecture
•	Layers
•	Environment variables
•	Default CMD
•	Entrypoint
•	Exposed ports
•	Working directory
Example to format nicely:
docker inspect nginx | less
Very useful for debugging image internals.
________________________________________
5️⃣ Remove an image you no longer need
First, make sure no containers are using it.
Then remove:
docker rmi alpine
If image is being used by a container:
docker rm <container_name>
docker rmi alpine
Force remove (careful):
docker rmi -f alpine
________________________________________
🔥 Quick Practice Flow
docker pull nginx ubuntu alpine
docker images
docker inspect alpine
docker rmi alpine
________________________________________

Task 2: Image Layers
1.	Run docker image history nginx — what do you see?
2.	Each line is a layer. Note how some layers show sizes and some show 0B
3.	Write in your notes: What are layers and why does Docker use them?

Great practical questions 👍 Let’s break this down clearly.
________________________________________
1️⃣ Run: docker image history nginx — What do you see?
When you run:
docker image history nginx
You’ll see something like this (simplified example):
IMAGE          CREATED        CREATED BY                         SIZE      COMMENT
abc123         2 weeks ago    CMD ["nginx" "-g" "daemon off;"]  0B
def456         2 weeks ago    EXPOSE 80                          0B
ghi789         2 weeks ago    RUN /bin/sh -c ...                 23MB
jkl012         2 weeks ago    ADD file:...                       150MB
...
You’ll notice:
•	Multiple rows
•	Each row has:
o	A command (RUN, ADD, CMD, etc.)
o	A size
o	A timestamp
•	Some layers show real size (MB)
•	Some layers show 0B
________________________________________
2️⃣ Each line is a layer — Why do some show size and some show 0B?
Every line represents a layer in the Docker image.
🔹 Layers with size (e.g., 23MB, 150MB)
These are layers that:
•	Added files
•	Installed packages
•	Modified filesystem content
Examples:
•	RUN apt-get install
•	ADD
•	COPY
These change the filesystem → so they consume space.
________________________________________
🔹 Layers with 0B
These are metadata-only layers.
Examples:
•	CMD
•	EXPOSE
•	ENV
•	WORKDIR
They don’t add files.
They only store configuration instructions.
So:
•	No filesystem change
•	No size added
•	Just image metadata
________________________________________
3️⃣ What are layers and why does Docker use them?
Here’s what you should write in your notes 👇
________________________________________
📌 What Are Docker Layers?
A Docker image is built as a stack of read-only layers.
Each instruction in a Dockerfile:
•	Creates a new layer
•	Builds on top of the previous layer
Think of it like:
Layer 4 → Your App
Layer 3 → Nginx Installed
Layer 2 → OS Packages
Layer 1 → Base OS (Debian/Alpine)
________________________________________
📌 Why Does Docker Use Layers?
Docker uses layers for:
1️⃣ Reusability
If two images use the same base image (like nginx), they share layers.
Example:
•	10 containers using nginx
•	They don’t store 10 copies
•	They share the same layers
👉 Saves disk space.
________________________________________
2️⃣ Caching (Faster Builds)
When building an image:
RUN apt-get update,    RUN apt-get install nginx
COPY . .
If only your code changes:
•	Docker reuses cached layers
•	Only rebuilds the changed layer
👉 Makes builds much faster.
________________________________________
3️⃣ Efficient Storage
Layers are:
•	Immutable (read-only)
•	Shared across containers
When a container runs:
•	Docker adds a thin writable layer on top
•	Original image layers remain unchanged
________________________________________
🔥 Real DevOps Insight
If you modify early layers in a Dockerfile:
FROM ubuntu
RUN apt-get update   ❌ changed
COPY . .
Docker must rebuild everything after that layer.
That’s why Dockerfile order matters for performance.
________________________________________
🧠 One-Line Summary for Your Notes
Docker layers are read-only filesystem snapshots created by each Dockerfile instruction. Docker uses them for caching, storage efficiency, and image reusability.
________________________________________

Task 3: Container Lifecycle
Practice the full lifecycle on one container:
1.	Create a container (without starting it)
2.	Start the container
3.	Pause it and check status
4.	Unpause it
5.	Stop it
6.	Restart it
7.	Kill it
8.	Remove it
Check docker ps -a after each step — observe the state changes.

Perfect 👍 This is full container lifecycle practice. I’ll use an nginx example container.
________________________________________
🐳 Docker Container Lifecycle – Step by Step
________________________________________
1️⃣ Create a container (without starting it)
docker create --name mynginx nginx
What happens?
•	Container is created
•	Filesystem + writable layer prepared
•	❌ Not running yet
Check status:
docker ps -a
You’ll see:
STATUS: Created
________________________________________
2️⃣ Start the container
docker start mynginx
Check:
docker ps
Now status:
Up X seconds
________________________________________
3️⃣ Pause it and check status
Pause:
docker pause mynginx
Check:
docker ps
Status will show:
Up X seconds (Paused)
👉 Pause freezes the container processes (like sending SIGSTOP).
________________________________________
4️⃣ Unpause it
docker unpause mynginx
Now:
Up X seconds
Container resumes execution.
________________________________________
5️⃣ Stop it
docker stop mynginx
What happens:
•	Sends SIGTERM
•	Waits gracefully
•	Then SIGKILL if needed
Check:
docker ps -a
Status:
Exited
________________________________________
6️⃣ Restart it
docker restart mynginx
This is equivalent to:
docker stop mynginx
docker start mynginx
Container will be:
Up X seconds
________________________________________
7️⃣ Kill it
docker kill mynginx
Difference from stop:
•	stop → graceful shutdown (SIGTERM)
•	kill → immediate SIGKILL (force stop)
Used when container is stuck.
________________________________________
8️⃣ Remove it
Container must be stopped first.
docker rm mynginx
If running, force remove:
docker rm -f mynginx
Now:
docker ps -a
Container is gone.
________________________________________
🧠 Status Flow Summary
Created → Running → Paused → Running → Exited → Running → Exited → Removed
________________________________________
🔥 Production Insight (DevOps-Level)
Command	When Used in Real Life
create	Rare (usually docker run used)
start	Restart stopped containers
pause	Debugging / resource control
stop	Normal shutdown
kill	Hung process
rm	Cleanup environments
________________________________________

Task 4: Working with Running Containers
1.	Run an Nginx container in detached mode
2.	View its logs
3.	View real-time logs (follow mode)
4.	Exec into the container and look around the filesystem
5.	Run a single command inside the container without entering it
6.	Inspect the container — find its IP address, port mappings, and mounts

Great — this is proper hands-on Docker practice 👌
We’ll use an Nginx container named web1.
________________________________________
🐳 1️⃣ Run an Nginx container in detached mode
docker run -d --name web1 -p 8080:80 nginx
What this does:
•	-d → detached (runs in background)
•	--name web1 → custom container name
•	-p 8080:80 → maps:
o	Host port 8080
o	Container port 80
Now open browser:
http://localhost:8080
You should see the Nginx welcome page.
________________________________________
📜 2️⃣ View its logs
docker logs web1
This shows:
•	Nginx startup messages
•	Access logs (if you hit the site)
________________________________________
🔴 3️⃣ View real-time logs (follow mode)
docker logs -f web1
Now:
•	Open browser again
•	Refresh the page
•	You’ll see live access logs
Press Ctrl + C to exit follow mode.
________________________________________
🖥 4️⃣ Exec into the container and explore filesystem
Enter interactive shell:
docker exec -it web1 /bin/bash
If bash is not available (some images use sh):
docker exec -it web1 /bin/sh
Now you are inside the container.
Explore:
ls /
ls /usr/share/nginx/html
cat /usr/share/nginx/html/index.html
That directory contains the default Nginx webpage.
Exit container:
exit
________________________________________
⚡ 5️⃣ Run a single command inside container (without entering)
Example:
docker exec web1 ls /usr/share/nginx/html
Or:
docker exec web1 cat /usr/share/nginx/html/index.html
This runs one command and exits.
________________________________________
🔍 6️⃣ Inspect the container
docker inspect web1
You’ll get a big JSON output.
________________________________________
📌 Find Container IP Address
Look for:
"NetworkSettings": {
    "IPAddress": "172.17.0.X"
}
Or cleaner:
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web1
________________________________________
📌 Find Port Mappings
Look for:
"Ports": {
    "80/tcp": [
        {
            "HostIp": "0.0.0.0",
            "HostPort": "8080"
        }
    ]
}
Meaning:
•	Host 8080 → Container 80
________________________________________
📌 Find Mounts (Volumes)
Look for:
"Mounts": []
If empty → no volumes attached.
If volumes exist, you’ll see:
•	Source (host path)
•	Destination (container path)
________________________________________
🧠 Quick DevOps Summary
Action	Command
Run detached	docker run -d
View logs	docker logs
Live logs	docker logs -f
Enter container	docker exec -it
Run single command	docker exec
Inspect details	docker inspect
________________________________________

Task 5: Cleanup
1.	Stop all running containers in one command
2.	Remove all stopped containers in one command
3.	Remove unused images
4.	Check how much disk space Docker is using
Excellent 🔥 — this is Docker cleanup & maintenance (very important in real DevOps environments).
________________________________________
🐳 1️⃣ Stop all running containers in one command
docker stop $(docker ps -q)
How it works:
•	docker ps -q → returns only container IDs of running containers
•	$(...) → passes them to docker stop
If no containers are running → nothing happens.
________________________________________
🗑 2️⃣ Remove all stopped containers in one command
docker container prune
Are you sure you want to continue? [y/N]
Force without confirmation:
docker container prune -f
________________________________________
🧹 3️⃣ Remove unused images
Remove dangling images (untagged layers):
docker image prune
Remove all unused images (not used by any container):
docker image prune -a
Force:
docker image prune -a -f
________________________________________
💾 4️⃣ Check how much disk space Docker is using
docker system df
Example output:
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          5         2         1.5GB     800MB
Containers      3         1         120MB     120MB
Local Volumes   2         1         500MB     200MB
Build Cache                             300MB
________________________________________
📊 Detailed view
docker system df -v
Shows:
•	Individual image sizes
•	Which containers use which images
•	Volume usage
•	Build cache usage
________________________________________
🚀 Nuclear Cleanup (Production Awareness)
If you want to remove everything unused:
docker system prune -a
Remove:
•	Stopped containers
•	Unused networks
•	Unused images
•	Build cache
⚠️ Be careful in production environments.
________________________________________
🧠 DevOps Best Practice
In CI/CD servers (like Jenkins, GitHub Actions runners):
You often schedule:
docker system prune -af
To prevent disk from filling up.
________________________________________
🔥 Quick Summary Table
Task	Command
Stop all running containers	docker stop $(docker ps -q)
Remove stopped containers	docker container prune
Remove unused images	docker image prune -a
Check disk usage	docker system df
Remove everything unused	docker system prune -a
________________________________________

Hints
•	Image history: docker image history
•	Create without starting: docker create
•	Follow logs: docker logs -f
•	Inspect: docker inspect
•	Cleanup: docker system df, docker system prune
