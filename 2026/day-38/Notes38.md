Day 38 – YAML Basics


Create person.yaml that describes yourself with: name role experience_years learning (a boolean)

name: ChatGPT
role: AI Assistant
experience_years: 0
learning: true

Add to person.yaml: tools — a list of 5 DevOps tools you know or are learning hobbies — a list using the inline format [item1, item2]

name: ChatGPT
role: AI Assistant
experience_years: 0
learning: true

tools:
  - Git
  - Docker
  - Kubernetes
  - Jenkins
  - Terraform

hobbies: [reading, coding]

Create server.yaml that describes a server: server with nested keys: name, ip, port database with nested keys: host, name, credentials (nested further: user, password)

server:
  name: web-server-01
  ip: 192.168.1.10
  port: 8080

database:
  host: db-server-01
  name: app_db
  credentials:
    user: db_user
    password: db_password

Task 4: Multi-line Strings
In server.yaml, add a startup_script field using:
1.	The | block style (preserves newlines)
2.	The > fold style (folds into one line)
Write in your notes: When would you use | vs >?

Here is the updated server.yaml with startup_script using both YAML block styles.
server:
  name: web-server-01
  ip: 192.168.1.10
  port: 8080

database:
  host: db-server-01
  name: app_db
  credentials:
    user: db_user
    password: db_password

startup_script_literal: |
  #!/bin/bash
  echo "Starting application"
  cd /app
  npm install
  npm start

startup_script_folded: >
  #!/bin/bash
  echo "Starting application"
  cd /app
  npm install
  npm start
What Happens
| Literal Block Style
•	Preserves line breaks exactly as written
•	Output remains multiple lines
Example result:
#!/bin/bash
echo "Starting application"
cd /app
npm install
npm start
> Folded Block Style
•	Folds line breaks into spaces
•	Output becomes one long line
Example result:
#!/bin/bash echo "Starting application" cd /app npm install npm start
When to Use | vs >
Use | when:
•	Writing scripts
•	Config files
•	Multi-line commands
•	When line breaks must be preserved
Example in DevOps:
•	Kubernetes init containers
•	Helm templates
•	Shell scripts in YAML
Use > when:
•	Writing long text
•	Descriptions
•	Messages
•	When you want clean wrapping but a single-line value
Example:
•	Kubernetes annotations
•	Documentation strings
✅ Simple rule:
•	| → keep formatting
•	> → fold into a single line
If you'd like, I can also show 3 tricky YAML interview questions DevOps engineers often fail (very common in Kubernetes configs).

Task 6: Spot the Difference
Read both blocks and write what's wrong with the second one:
# Block 1 - correct
name: devops
tools:
  - docker
  - kubernetes
# Block 2 - broken
name: devops
tools:
- docker
  - kubernetes
ANS
What is wrong
1.	- docker is not indented under tools:
o	It starts at the same level as tools:.
o	YAML may interpret this incorrectly because it does not clearly belong to the tools key.
2.	Inconsistent indentation
o	- docker has 0 spaces
o	- kubernetes has 2 spaces
o	YAML requires consistent indentation for list items.
Correct version of Block 2
name: devops
tools:
  - docker
  - kubernetes

