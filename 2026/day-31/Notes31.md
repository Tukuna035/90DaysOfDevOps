Day 31 – Dockerfile: Build Your Own Images

Task 1: Your First Dockerfile
1.	Create a folder called my-first-image
2.	Inside it, create a Dockerfile that:
o	Uses ubuntu as the base image
o	Installs curl
o	Sets a default command to print "Hello from my custom image!"
3.	Build the image and tag it my-ubuntu:v1
4.	Run a container from your image
Perfect 👌 Let’s build your first custom Docker image step by step.
________________________________________
🗂 1️⃣ Create a folder
mkdir my-first-image
cd my-first-image
________________________________________
📄 2️⃣ Create a Dockerfile
Create a file named exactly:
touch Dockerfile
Now open it and add:
FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/*

CMD ["echo", "Hello from my custom image!"]
________________________________________
🔎 What this does
•	FROM ubuntu:latest → Base image is Ubuntu
•	RUN apt-get update && apt-get install -y curl → installs curl
•	rm -rf /var/lib/apt/lists/* → reduces image size
•	CMD → default command when container runs
________________________________________
🏗 3️⃣ Build the image
Run this inside my-first-image folder:
docker build -t my-ubuntu:v1 .
Explanation:
•	-t → tag the image
•	my-ubuntu:v1 → image name + version tag
•	. → current directory (where Dockerfile is located)
Check image:
docker images
You should see:
my-ubuntu   v1
________________________________________
🚀 4️⃣ Run a container from your image
docker run my-ubuntu:v1
Output:
Hello from my custom image!
Container will exit immediately after printing the message (because echo finishes).
________________________________________

Task 2: Dockerfile Instructions
Create a new Dockerfile that uses all of these instructions:
•	FROM — base image
•	RUN — execute commands during build
•	COPY — copy files from host to image
•	WORKDIR — set working directory
•	EXPOSE — document the port
•	CMD — default command
Build and run it. Understand what each line does.

Excellent 🔥 — this is where Dockerfile concepts come together.
We’ll create a simple Python web app image that uses ALL required instructions.
________________________________________
📁 1️⃣ Create Project Structure
mkdir docker-full-example
cd docker-full-example
Create these files:
touch Dockerfile app.py requirements.txt
________________________________________
📝 2️⃣ Create app.py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from full Dockerfile example!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
________________________________________
📦 3️⃣ Create requirements.txt
flask
________________________________________
🐳 4️⃣ Create Dockerfile (Uses ALL Required Instructions)
# 1️⃣ Base image
FROM python:3.10-slim

# 2️⃣ Set working directory
WORKDIR /app

# 3️⃣ Copy files from host to image
COPY requirements.txt .
COPY app.py .

# 4️⃣ Install dependencies during build
RUN pip install --no-cache-dir -r requirements.txt

# 5️⃣ Document the port
EXPOSE 5000

# 6️⃣ Default command
CMD ["python", "app.py"]
________________________________________
🔍 What Each Instruction Does
Instruction	Purpose
FROM	Base OS + Python runtime
WORKDIR	Sets /app as working directory
COPY	Copies files into image
RUN	Installs Flask during build
EXPOSE	Documents port 5000
CMD	Starts the Flask app
________________________________________
🏗 5️⃣ Build the Image
docker build -t full-docker-example:v1 .
________________________________________
🚀 6️⃣ Run the Container
docker run -d -p 5000:5000 --name flask-app full-docker-example:v1
Open browser:
http://localhost:5000
You’ll see:
Hello from full Dockerfile example!
________________________________________

Task 3: CMD vs ENTRYPOINT
1.	Create an image with CMD ["echo", "hello"] — run it, then run it with a custom command. What happens?
2.	Create an image with ENTRYPOINT ["echo"] — run it, then run it with additional arguments. What happens?
3.	Write in your notes: When would you use CMD vs ENTRYPOINT?

Excellent 🔥 This is one of the most important Docker concepts.
Let’s test both practically and then understand the difference deeply.
________________________________________
🧪 1️⃣ Image with CMD ["echo", "hello"]
________________________________________
📄 Dockerfile
FROM ubuntu:latest
CMD ["echo", "hello"]
Build it:
docker build -t cmd-test:v1 .
________________________________________
▶ Run without custom command
docker run cmd-test:v1
Output:
hello
✔ It runs the default CMD.
________________________________________
▶ Run with custom command
docker run cmd-test:v1 echo "custom message"
Output:
custom message
👉 What happened?
Docker replaced the CMD entirely.
CMD is overridden when you pass a command in docker run.
________________________________________
🧪 2️⃣ Image with ENTRYPOINT ["echo"]
________________________________________
📄 Dockerfile
FROM ubuntu:latest
ENTRYPOINT ["echo"]
Build:
docker build -t entrypoint-test:v1 .
________________________________________
▶ Run without arguments
docker run entrypoint-test:v1
Output:
(Empty line — because echo ran with no arguments.)
________________________________________
▶ Run with additional arguments
docker run entrypoint-test:v1 hello world
Output:
hello world
👉 What happened?
Docker did NOT replace ENTRYPOINT.
Instead, it appended the arguments:
Internally this became:
echo hello world
________________________________________
🧠 Core Difference
Feature	CMD	ENTRYPOINT
Can be overridden?	✅ Yes (completely replaced)	❌ No (arguments appended)
Purpose	Default command	Fixed executable
Best for	Flexible containers	Tool-style containers
________________________________________
🔥 Bonus: CMD + ENTRYPOINT Together
Example:
FROM ubuntu:latest
ENTRYPOINT ["echo"]
CMD ["hello"]
Now:
docker run image-name
Output:
hello
If you run:
docker run image-name world
Output:
world
Here:
•	ENTRYPOINT = fixed command
•	CMD = default arguments
Very powerful pattern.
________________________________________
📝 3️⃣ What to Write in Your Notes
Here’s a clean explanation 👇
________________________________________
When to Use CMD vs ENTRYPOINT
Use CMD when:
•	You want a default command
•	But allow users to override it easily
•	Example: testing, development containers
Use ENTRYPOINT when:
•	The container should behave like a fixed executable
•	You don’t want the base command replaced
•	Example: CLI tools, database containers
________________________________________
🚀 Real-World Examples
Nginx
Uses ENTRYPOINT so it always runs nginx.
MySQL
Uses ENTRYPOINT to ensure database always starts properly.
________________________________________
🧠 One-Line Summary
CMD provides default arguments that can be overridden. ENTRYPOINT defines the main executable that always runs.
________________________________________
🧠 Think Like This
•	CMD = Default instruction (can be replaced)
•	ENTRYPOINT = Fixed instruction (cannot be replaced, only extended)

Task 4: Build a Simple Web App Image
1.	Create a small static HTML file (index.html) with any content
2.	Write a Dockerfile that:
o	Uses nginx:alpine as base
o	Copies your index.html to the Nginx web directory
3.	Build and tag it my-website:v1
4.	Run it with port mapping and access it in your browser

Perfect 👌 Let’s build your own custom Nginx website image step by step.
________________________________________
📁 1️⃣ Create Project Folder
mkdir my-website
cd my-website
________________________________________
📄 2️⃣ Create index.html
touch index.html
Add some content:
<!DOCTYPE html>
<html>
<head>
    <title>My First Docker Website</title>
</head>
<body>
    <h1>Hello from my custom Nginx container 🚀</h1>
    <p>This website is running inside Docker!</p>
</body>
</html>
Save the file.
________________________________________
🐳 3️⃣ Create Dockerfile
touch Dockerfile
Add this:
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
________________________________________
🔎 What this does
•	FROM nginx:alpine → Uses lightweight Nginx image
•	COPY → Replaces default Nginx page with your custom page
The default Nginx web root directory is:
/usr/share/nginx/html
________________________________________
🏗 4️⃣ Build the Image
docker build -t my-website:v1 .
Check:
docker images
You should see:
my-website   v1
________________________________________
🚀 5️⃣ Run the Container with Port Mapping
docker run -d -p 8080:80 --name website-container my-website:v1
Explanation:
•	-d → run in background
•	-p 8080:80
o	Host port 8080
o	Container port 80 (Nginx default)
________________________________________
🌐 6️⃣ Access in Browser
Open:
http://localhost:8080
You should see:
Hello from my custom Nginx container 🚀
This website is running inside Docker!
🎉 Congratulations — you just containerized a website.
________________________________________
🧠 Extra (Optional Debugging)
Check logs:
docker logs website-container
Exec inside:
docker exec -it website-container sh
Check file:
ls /usr/share/nginx/html
________________________________________
🔥 What You Just Learned
You used:
•	FROM
•	COPY
•	docker build
•	docker run
•	Port mapping
•	Static site deployment with Nginx
That’s real-world DevOps skill 🚀
________________________________________

Task 5: .dockerignore
1.	Create a .dockerignore file in one of your project folders
2.	Add entries for: node_modules, .git, *.md, .env
3.	Build the image — verify that ignored files are not included

Here’s a simple step-by-step practical guide you can run inside any of your Docker project folders.
________________________________________
✅ 1️⃣ Create a .dockerignore file
Inside your project root (where your Dockerfile exists):
touch .dockerignore
Open it and add:
node_modules
.git
*.md
.env
What each line does:
•	node_modules → ignores dependency folder
•	.git → excludes git history
•	*.md → ignores all markdown files
•	.env → prevents secrets from being copied
________________________________________
✅ 2️⃣ Build the Docker image
From the same directory:
docker build -t my-test-image .
Watch the first few lines of output carefully. You should see something like:
Sending build context to Docker daemon  XX.XkB
👉 If .dockerignore works, the build context size will be small (node_modules won’t be sent).
If it’s very large (MBs or GBs), your .dockerignore isn’t working properly.
________________________________________
✅ 3️⃣ Verify ignored files are NOT inside the image
Run a container:
docker run -it --rm my-test-image sh
Now check:
ls -a
You should NOT see:
•	node_modules
•	.git
•	.env
•	Any .md files
________________________________________
🔎 Extra Verification (Advanced but Useful)
You can also check image layers:
docker history my-test-image
Or inspect image size:
docker images
If .dockerignore is working properly:
•	Image size is smaller
•	Build is faster
•	Sensitive files are excluded
________________________________________
🚀 Why This Is Important (DevOps Perspective)
Without .dockerignore:
•	Your image becomes large
•	Builds become slow
•	Secrets might leak
•	CI/CD pipelines become inefficient
This is a very common real-world interview question.
________________________________________


Task 6: Build Optimization
1.	Build an image, then change one line and rebuild — notice how Docker uses cache
2.	Reorder your Dockerfile so that frequently changing lines come last
3.	Write in your notes: Why does layer order matter for build speed?


Great — this is a very important Docker concept 🔥 (layer caching optimization).
Let’s do it step-by-step like a real DevOps engineer.
________________________________________
🧪 Part 1 — Build Image and Observe Cache
Step 1️⃣ Create a simple Dockerfile
Example (Node.js app):
FROM node:18

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

CMD ["node", "app.js"]
________________________________________
Step 2️⃣ Build the image
docker build -t cache-demo .
You’ll see something like:
Step 1/6 : FROM node:18
 ---> Using cache
Step 2/6 : WORKDIR /app
 ---> Using cache
Step 3/6 : COPY package.json .
 ---> Using cache
Step 4/6 : RUN npm install
 ---> Using cache
Step 5/6 : COPY . .
 ---> Using cache
First build: no cache
Second build (without changes): everything shows Using cache
________________________________________
Step 3️⃣ Change One Line
Open app.js and change something small:
console.log("Hello Docker v2");
Now rebuild:
docker build -t cache-demo .
You’ll notice:
Step 1/6 : FROM node:18
 ---> Using cache
Step 2/6 : WORKDIR /app
 ---> Using cache
Step 3/6 : COPY package.json .
 ---> Using cache
Step 4/6 : RUN npm install
 ---> Using cache
Step 5/6 : COPY . .
 ---> NOT using cache
👉 Docker only rebuilt from the changed layer downward.
That is Docker layer caching.
________________________________________
⚠️ Now Let’s See a Bad Dockerfile Order
Bad version:
FROM node:18

WORKDIR /app

COPY . .

RUN npm install

CMD ["node", "app.js"]
Problem:
If you change even one JS file, Docker must:
•	Re-copy everything
•	Re-run npm install
•	Rebuild everything
This is slow ❌
________________________________________
✅ Optimized Dockerfile (Correct Order)
FROM node:18

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm install

COPY . .

CMD ["node", "app.js"]
Now:
•	If source code changes → only last layer rebuilds
•	If dependencies change → npm install runs again
Much faster 🚀
________________________________________
🧠 Your Notes Answer
Why does layer order matter for build speed?
Docker builds images layer by layer.
Each instruction in a Dockerfile creates a new immutable layer.
If a layer changes:
•	That layer and all layers after it must rebuild.
•	Layers before it are reused from cache.
Therefore:
👉 Frequently changing instructions should be placed at the bottom.
👉 Stable instructions (like dependency installation) should be placed at the top.
This maximizes cache reuse and reduces build time.
________________________________________
🔥 Simple Rule to Remember
Stable stuff → Top
Changing stuff → Bottom
Dependencies before source code
Environment setup before app logic
________________________________________
🚀 Real-World Impact
In CI/CD pipelines:
•	Bad layer order = 5–10 minute builds
•	Good layer order = 30–60 second builds
Huge productivity difference.
________________________________________
Hints
•	Build: docker build -t name:tag .
•	The . at the end is the build context
•	COPY . . copies everything from host to container
•	Nginx serves files from /usr/share/nginx/html/


