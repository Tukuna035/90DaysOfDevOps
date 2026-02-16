

Day 22 – Introduction to Git: Your First Repository

what Git is and why it matters?

Git is a distributed version control system (DVCS) used to track changes in source code during software development.
It was created in 2005 by Linus Torvalds (the creator of Linux).
In simple words:
Git is a tool that remembers every change you make in your project.
________________________________________
📦 What is Version Control?


Version control means:
•	Tracking changes in files
•	Going back to older versions if something breaks
•	Seeing who changed what and when
•	Working safely with multiple developers
Without Git:
•	You rename files like:
•	project_v1
•	project_final
•	project_final_new
•	project_final_last_really_final
With Git:
•	Everything is tracked automatically and cleanly.
________________________________________
⚙️ Why Git Matters (Very Important)


1️⃣ Prevents Code Loss
If you delete or break something:
git checkout <old-version>
You can restore it.
No more panic.
________________________________________
2️⃣ Enables Team Collaboration
Multiple developers can:
•	Work on different features
•	Merge changes safely
•	Avoid overwriting each other’s code
This is critical in companies using platforms like GitHub.
________________________________________
3️⃣ Branching = Safe Experimentation 🌿
You can create branches:
git branch new-feature
Work on features without touching production code.
This is the backbone of:
•	DevOps
•	CI/CD
•	Agile development
________________________________________
4️⃣ Required for DevOps & Cloud Roles
Since you're learning DevOps, Git is:
•	Used in CI/CD pipelines
•	Required for automation
•	Core skill for production engineers
•	Essential for tools like Jenkins, Kubernetes deployments, etc.
No Git → No DevOps.
________________________________________
5️⃣ Distributed = Works Offline
Unlike older systems:
•	Every developer has a full copy of the repository.
•	You can commit offline.
•	Faster and more secure.
________________________________________
🧠 Simple Real-World Example
Imagine you're building an application:
Without Git:
•	You edit files
•	Something breaks
•	You don’t know what changed
With Git:
git log
You see full history.
git diff
You see exact changes.
________________________________________
🔥 Why Companies Love Git


Because it provides:
•	Speed
•	Reliability
•	Full history
•	Team collaboration
•	Easy rollback
•	Integration with CI/CD
That’s why almost every tech company uses Git.
________________________________________
🚀 In One Line


Git is the backbone of modern software development.
what are most used git commands ?
Great question 👍
If you're learning DevOps or working as a production/support engineer, these are the most used Git commands in real-world projects.
________________________________________
🔥 Most Used Git Commands (Daily Use)


1️⃣ git init
Initialize a new Git repository.
git init
Used when starting a new project.
________________________________________
2️⃣ git clone
Copy a remote repository to your local machine.
git clone https://github.com/user/repo.git
Example: Cloning a project from GitHub
________________________________________
3️⃣ git status
Shows current state of your working directory.
git status
Very frequently used.
________________________________________
4️⃣ git add
Add files to staging area.
git add .
or specific file:
git add app.js
________________________________________
5️⃣ git commit
Save changes with a message.
git commit -m "Fixed login issue"
This creates a snapshot in Git.
________________________________________
6️⃣ git push
Upload local commits to remote repository.
git push
Used after committing changes.
________________________________________
7️⃣ git pull
Download latest changes from remote repository.
git pull
Very important before starting work.
________________________________________
8️⃣ git branch
Check or create branches.
git branch
Create new branch:
git branch feature-login
________________________________________
9️⃣ git checkout
Switch between branches.
git checkout feature-login
Or create + switch:
git checkout -b feature-login
________________________________________
🔟 git merge
Merge one branch into another.
git merge feature-login
Used after feature development.
________________________________________
🧠 Intermediate But Very Important

🔹 git log
View commit history.
git log
________________________________________
🔹 git diff
See what changed.
git diff
________________________________________
🔹 git stash
Temporarily save changes.
git stash
Very useful in production support situations.
________________________________________
🔹 git remote -v
Check connected remote repository.
git remote -v
________________________________________
🚀 Real-World Daily Workflow

git pull
git checkout -b new-feature
git add .
git commit -m "Added new feature"
git push
________________________________________
🎯 If You’re in DevOps / Production Support
Most important commands to master:


•	git pull
•	git push
•	git add
•	git commit
•	git branch
•	git checkout
•	git log
•	git diff
•	git stash
These are used almost every day in real projects.


How to do ssh in local machine to connect github to do push and pull ?
Perfect 🔥 this is the right way to connect your local machine to GitHub — using SSH (more secure, no password every time).
We’ll do this step-by-step.
________________________________________
🧠 What We’re Doing

We will:
1.	Generate SSH key on local machine
2.	Add SSH key to GitHub
3.	Test connection
4.	Push & Pull using SSH
________________________________________
✅ STEP 1: Check if SSH Key Already Exists
Open terminal:
ls ~/.ssh
If you see files like:
id_rsa
id_rsa.pub
id_ed25519
id_ed25519.pub
You may already have a key.
If not → generate one.
________________________________________
✅ STEP 2: Generate New SSH Key
Recommended (modern & secure):
ssh-keygen -t ed25519 -C "your_email@example.com"
Press Enter for default location.
Press Enter for empty passphrase (or set one if you want security).
It will create:
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
________________________________________
✅ STEP 3: Start SSH Agent
eval "$(ssh-agent -s)"
Add your key:
ssh-add ~/.ssh/id_ed25519
________________________________________
✅ STEP 4: Copy Public Key
cat ~/.ssh/id_ed25519.pub
Copy the full output (starts with ssh-ed25519).
________________________________________
✅ STEP 5: Add SSH Key to GitHub
Go to:
GitHub → Settings → SSH and GPG Keys → New SSH Key
Paste your copied key → Save.
________________________________________
✅ STEP 6: Test SSH Connection
Run:
ssh -T git@github.com
If successful, you’ll see:
Hi username! You've successfully authenticated.
🔥 That means SSH is working.
________________________________________
✅ STEP 7: Use SSH Remote URL
Instead of HTTPS:
❌ HTTPS:
https://github.com/username/repo.git
✅ SSH:
git@github.com:username/repo.git
________________________________________
Change Existing Repo to SSH
Inside your project:
git remote set-url origin git@github.com:username/repo.git
Verify:
git remote -v
________________________________________
🚀 Now Push & Pull Normally
git push
git pull
No password needed anymore 🎉
________________________________________
🔥 Quick Full Setup Summary
ssh-keygen -t ed25519 -C "email"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519"
cat ~/.ssh/id_ed25519.pub
Add to GitHub → Test → Use SSH URL.


 
 

How to push file from local to GitHub after ssh?

Step-by-Step Instructions
1.	Stage your files for the first commit:
             git add .
2.	Commit the staged files with a descriptive message:
            git commit -m "First commit"
3.	Push the changes from your local repository to GitHub:
              git push -u origin main

What is the difference between git add and git commit?

Good 👌 this is a core Git concept — if you understand this clearly, Git becomes easy.
We’ll keep it simple and practical.
________________________________________
🧠 First Understand 3 Areas in Git
In Git, your project has 3 stages:
1️⃣ Working Directory → where you edit files
2️⃣ Staging Area (Index) → where you prepare changes
3️⃣ Repository (.git) → where commits are permanently stored
Think of it like:
Edit → Select → Save permanently
________________________________________
🔵 What git add Does
git add file.txt
👉 Moves changes from Working Directory → Staging Area
It does NOT save permanently.
It only says:
“I want this file included in the next commit.”
You can stage:
git add .
(All files)
________________________________________
🟢 What git commit Does
git commit -m "Added login feature"
👉 Moves changes from Staging Area → Git Repository
This creates a permanent snapshot in Git history.
Now Git remembers:
•	What changed
•	Who changed it
•	When it changed
Key Difference (Very Important)
git add	git commit
Prepares changes	Saves changes permanently
Moves to staging	Creates snapshot
Can select specific files	Saves whatever is staged
Not permanent	Permanent record

Why Doesn’t Git Just Commit Directly?
Because real development is messy.
If Git committed everything automatically, your history would be:
commit 1: random changes
commit 2: more random changes
commit 3: half feature
That’s messy and unprofessional.
________________________________________
🚀 Git’s Design Philosophy
Git was designed by Linus Torvalds for the Linux kernel — a project with thousands of developers.
They needed:
•	Clean history
•	Precise commits
•	Logical grouping of changes
The staging area makes that possible.
🧠 What Does git log Show?
git log shows the history of commits in your repository.
Run:
git log
You’ll see something like:
commit 9fceb02f9d5b3a1e7e8c...
Author: John Doe <john@example.com>
Date:   Mon Feb 15 10:30:12 2026 +0530

    Fixed login validation bug
________________________________________
📌 Information It Shows
1️⃣ Commit Hash (SHA-1)
Example:
commit 9fceb02f9d5b3a1e7e8c...
•	A unique 40-character ID
•	Identifies that exact snapshot
•	Used for checkout, revert, reset, etc.
You can reference it like:
git checkout 9fceb02
________________________________________
2️⃣ Author
Author: John Doe <john@example.com>
Tells you:
•	Who made the change
•	Their configured email
Important in team environments like GitHub.
________________________________________
3️⃣ Date & Time
Date: Mon Feb 15 10:30:12 2026
Shows when the commit was created.
Useful for:
•	Debugging production issues
•	Tracking when bugs were introduced
________________________________________
4️⃣ Commit Message
Fixed login validation bug
This explains why the change was made.
Good teams write:
•	Clear
•	Specific
•	Action-oriented messages
Bad example:
fixed stuff
Good example:
Fixed null pointer exception in payment service
________________________________________
🔥 Very Useful Variations of git log
🔹 Compact View
git log --oneline
Output:
9fceb02 Fixed login bug
ab23e11 Added payment API
Perfect for quick history overview.
________________________________________
🔹 Show Graph (Branches Visualized)
git log --oneline --graph --all
Shows branching and merging visually.
Very useful in DevOps workflows.
________________________________________
🔹 Show Changes in Each Commit
git log -p
Displays full code changes (diffs).
________________________________________
🔹 Limit Results
git log -5
Shows last 5 commits.
________________________________________
🎯 Why git log Is Important
In real production:
If something breaks, you ask:
•	What changed?
•	Who changed it?
•	When did it change?
git log answers all of that.
________________________________________
🧠 In One Line
git log shows the full history of commits — who changed what and when.
________________________________________
What is the .git/ folder and what happens if you delete it?
Ahhh now we’re opening the engine of Git 🚀
This is where things get real.
We’re talking about the hidden .git/ folder inside a project managed by Git.
________________________________________
🧠 What Is the .git/ Folder?
When you run:
git init
Git creates a hidden folder:
.git/
This folder is the entire brain of your repository.
It stores:
•	All commit history
•	All branches
•	All tags
•	Configuration
•	Remote URLs
•	Staged data
•	Object database (blobs, trees, commits)
Without .git/, Git is just normal files.
________________________________________
📦 What’s Inside .git/?
If you run:
ls -a .git
You’ll see folders like:
objects/
refs/
HEAD
config
index
logs/
🔹 objects/
Stores all Git data (compressed snapshots).
Git doesn’t store “file changes” like other systems.
It stores snapshots.
________________________________________
🔹 refs/
Stores branch pointers.
Example:
refs/heads/main
That file points to the latest commit hash.
________________________________________
🔹 HEAD
Tells Git which branch you are currently on.
________________________________________
🔹 index
This is your staging area file.
When you run:
git add
It updates this file.
________________________________________
🔹 config
Stores repository configuration (remotes, settings).
________________________________________
🎯 So What Happens If You Delete .git/?
Let’s say you do this:
rm -rf .git
💥 What happens?
Your project becomes:
•	❌ Not a Git repository anymore
•	❌ All commit history gone
•	❌ All branches gone
•	❌ Remote connection gone
•	❌ Staging area gone
Your files remain.
But Git tracking is completely destroyed.
It becomes just a normal folder.
________________________________________
🔥 Important Detail
If you had pushed your code to GitHub, the remote repo still has the history.
You can recover by:
git clone <repo-url>
But if you never pushed…
👉 The history is permanently lost.
________________________________________
🧠 Simple Analogy
Your project folder = Body
.git/ folder = Brain
Delete the brain → body still exists, but memory is gone.
________________________________________
🚀 Why This Matters in DevOps
•	.git/ contains deployment history
•	CI/CD pipelines depend on commit metadata
•	Branch-based workflows rely on refs inside .git/
Understanding this helps you debug:
•	Detached HEAD issues
•	Corrupted repo problems
•	Broken branch references
________________________________________
🎯 In One Line
.git/ is the complete database of your repository. Delete it, and Git forgets everything.
________________________________________
What is the difference between a working directory, staging area, and repository? 
Perfect 👌 this is the core foundation of how Git works.
If you truly understand these three, Git becomes very simple.
________________________________________
🧠 The 3 Main Areas in Git
Working Directory  →  Staging Area  →  Repository
Let’s break them down clearly.
________________________________________
1️⃣ Working Directory (Your Actual Files)
This is:
•	The folder on your computer
•	Where you create/edit/delete files
•	What you see in VS Code or terminal
Example:
You open app.js and change code.
That change exists only in your working directory.
Git knows something changed, but it is NOT saved in history yet.
Check with:
git status
________________________________________
2️⃣ Staging Area (Preparation Zone)
Also called the index.
When you run:
git add app.js
You move changes from:
Working Directory → Staging Area
This means:
“I want this file included in the next commit.”
Important:
•	Changes are selected
•	Not permanent yet
•	You can still modify them
Think of it like selecting items before checkout.
________________________________________
3️⃣ Repository (Permanent History)
When you run:
git commit -m "Updated login logic"
You move changes from:
Staging Area → Repository
Now:
•	A permanent snapshot is created
•	A commit hash is generated
•	History is updated
•	The change is saved inside .git/
This is stored in Git’s internal database.
