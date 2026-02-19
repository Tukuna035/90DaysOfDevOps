Day 23 – Git Branching & Working with GitHub

How to connect local to GitHub using personal token GitHub?
Step 1: Generate a Personal Access Token (PAT) on GitHub 
1.	Sign in to your account on GitHub.
2.	Click your profile photo in the top-right corner, then click Settings.
3.	In the left sidebar, click Developer settings.
4.	In the left sidebar, under "Personal access tokens", select Tokens (classic).
5.	Click the Generate new token button, and then select Generate new token (classic). (GitHub recommends fine-grained tokens for better security, but classic tokens are often simpler for basic use cases).
6.	Give your token a descriptive Note (e.g., "My personal laptop access") and set an Expiration date.
7.	Select the necessary scopes or permissions. For typical repository operations (read/write), select the repo scope.
8.	Click Generate token at the bottom of the page.
9.	Crucially, copy the generated token immediately. You will not be able to see it again once you leave the page, so save it in a secure place. 

Step 2: Use the PAT to Connect your Local Repository 
You can connect an existing local repository or clone a new one. 
Option A: For an existing local repository
1.	Open your terminal or command prompt and navigate to your local repository's root directory.
2.	git remote set-url origin 

ubuntu@ip-172-31-18-163:~/devops-nginx-demo$ git remote -v
origin  https://github.com/Tukuna035/devops-nginx-demo.git (fetch)
origin  https://github.com/Tukuna035/devops-nginx-demo.git (push)
ubuntu@ip-172-31-18-163:~/devops-nginx-demo$ git remote set-url origin https://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@github.com/Tukuna035/devops-nginx-demo.git
 






=====================================================================
What is a branch in Git?
🌿 What Is a Branch in Git?
A branch in Git is a separate line of development.
It allows you to:
•	Work on new features
•	Fix bugs
•	Experiment safely
•	Without affecting the main code
Think of a branch like a parallel copy of your project where you can make changes independently.
________________________________________
🧠 Why Branches Matter
In real projects (especially on platforms like GitHub):
•	main (or master) = stable production code
•	feature-login = new feature
•	bugfix-payment = bug fix
•	release-v1.1 = release preparation
This keeps work organized and safe.
________________________________________
📌 How Branch Works Internally
A branch is just a pointer to a commit.
Example:
A --- B --- C   (main)
If you create a branch:
A --- B --- C   (main)
              \
               D --- E   (feature)
Now:
•	main points to C
•	feature points to E
They are independent until merged.
________________________________________
🛠️ Common Branch Commands
🔹 Create a branch
git branch feature-login
🔹 Switch to branch
git checkout feature-login
Or modern way:
git switch feature-login
🔹 Create + switch together
git checkout -b feature-login
🔹 List branches
git branch
🔹 Delete branch
git branch -d feature-login
________________________________________
🚀 Real-World Example (Team Workflow)
1.	Developer creates a branch
2.	Works on feature
3.	Pushes to GitHub
4.	Creates Pull Request
5.	Team reviews
6.	Merge into main
________________________________________
🎯 Simple Definition (Interview Ready)
A branch in Git is a lightweight pointer to a commit that allows parallel development without affecting the main codebase.


Why do we use branches instead of committing everything to main?
Great question 👍 — this is something interviewers love to ask.
🌿 Why Not Just Commit Everything to main in Git?
Because main is usually the stable, production-ready branch.
If everyone commits directly to main, problems happen.
Let’s break it down.
________________________________________
🚨 Problems If Everyone Commits to main
1️⃣ Production Can Break
If you commit unfinished code:
•	Application may crash
•	Features may not work
•	Users get errors
main should always be deployable.
________________________________________
2️⃣ No Safe Experimentation
What if you want to:
•	Try a new feature?
•	Refactor code?
•	Test something risky?
Without branches:
•	You risk breaking stable code.
With branches:
•	You experiment safely.
•	If it fails → delete branch.
________________________________________
3️⃣ Team Collaboration Becomes Messy
Imagine 5 developers pushing to main:
•	Conflicts increase
•	Code becomes unstable
•	No proper review process
Branches allow:
•	Feature isolation
•	Pull Requests
•	Code reviews
•	CI/CD validation
Especially when using platforms like GitHub.
________________________________________
4️⃣ Cleaner Code Reviews
With branches:
•	One branch = one feature
•	Easy to review
•	Easy to revert if needed
Without branches:
•	Mixed commits
•	Hard to track changes
________________________________________
5️⃣ Better CI/CD Pipelines
In real DevOps workflow:
•	main → Production
•	develop → Staging
•	feature/* → Development
•	hotfix/* → Emergency fixes
Branches support structured deployment pipelines.

================================================================


How merge works in GitHub?

🔀 How Merge Works in GitHub
Merging in GitHub means combining changes from one branch into another branch.
Most common example:
•	You create a feature branch
•	You work on new code
•	Then you merge it into the main branch
________________________________________
🧠 Basic Idea of Merge (Git Concept)
Git tracks changes using commits.
When you merge:
•	Git compares the histories of two branches
•	Finds the common ancestor commit
•	Combines the changes
•	Creates a new merge commit (in most cases)
________________________________________
🌿 Example Workflow
1️⃣ Create a branch
git checkout -b feature-login
2️⃣ Make changes and commit
git add .
git commit -m "Added login feature"
3️⃣ Merge into main
git checkout main
git merge feature-login
Now your main branch contains the feature.
________________________________________
🔥 How Merge Works on GitHub Website (Pull Request)
On GitHub, merging usually happens via Pull Request (PR).
Steps:
1.	Push your branch:
git push origin feature-login
2.	Go to GitHub
3.	Click Compare & Pull Request
4.	Review changes
5.	Click Merge Pull Request
GitHub then merges the branch into main.
________________________________________
⚙️ Types of Merge in GitHub
When merging a PR, GitHub gives 3 options:
1️⃣ Create a Merge Commit (Default)
•	Keeps full history
•	Creates a new merge commit
•	Good for tracking branch history
2️⃣ Squash and Merge
•	Combines all commits into one
•	Cleaner history
•	Common in professional projects
3️⃣ Rebase and Merge
•	Rewrites commit history
•	Linear history (no merge commit)
•	Advanced usage
________________________________________
🚨 What is a Merge Conflict?
A conflict happens when:
•	Two branches change the same line in a file
Example:
Branch A:
let name = "Rahul";
Branch B:
let name = "Ravi";
Git doesn’t know which one to keep → conflict.
You must:
1.	Open file
2.	Manually fix
3.	git add
4.	git commit
________________________________________
📊 Visual Representation
main:     A ---- B ---- C
                   \
feature:            D ---- E
After merge:
main:     A ---- B ---- C -------- M
                   \              /
feature:            D ---- E -----
M = merge commit
________________________________________
🎯 Why Merging is Important
•	Combine team work
•	Integrate features
•	Release updates
•	Maintain structured development
===========================================================================
What Is HEAD in Git?
HEAD is a pointer to your current position in the repository.
In simple words:
HEAD tells Git which commit you are currently working on.
________________________________________
📌 Normally, HEAD Points to a Branch
Most of the time:
HEAD → main → Commit C
That means:
•	You are on the main branch
•	The latest commit of main is your current working position
You can verify with:
git branch
The branch with * is where HEAD is pointing.
________________________________________
🔎 What Happens Internally?
Inside the .git/HEAD file, you’ll usually see something like:
ref: refs/heads/main
That means:
•	HEAD points to the main branch
•	main points to the latest commit
So technically:
HEAD → Branch → Commit
________________________________________
⚠️ What Is Detached HEAD?
If you checkout a specific commit:
git checkout <commit-id>
Now:
HEAD → Commit (not branch)
This is called Detached HEAD state.
In this state:
•	You are not on any branch
•	New commits won’t belong to a branch unless you create one
To fix it:
git switch -c new-branch-name
________________________________________
🛠️ Common HEAD Usage Examples
🔹 See last commit
git show HEAD
🔹 Previous commit
git show HEAD~1
🔹 Reset to last commit
git reset --hard HEAD
________________________________________
📊 Visual Example
A --- B --- C   (main)
              ↑
            HEAD
If you switch branch:
A --- B --- C   (main)
       \
        D --- E   (feature)
                 ↑
               HEAD
________________________________________
🎯 Simple Interview Definition
HEAD in Git is a special pointer that indicates the currently checked-out branch or commit.


What happens to your files when you switch branches?

When you switch branches in Git, your project files change to match the snapshot stored in the branch you’re switching to.
Let’s break it down clearly 👇
________________________________________
🔄 1️⃣ Your Working Directory Is Updated
Every branch points to a specific commit (a snapshot of your project at that time).
When you run:
git switch branch-name
or
git checkout branch-name
Git:
•	Replaces modified files with the versions from that branch
•	Adds files that exist in the new branch
•	Removes files that don’t exist in the new branch
👉 Your project folder now looks exactly like it did in that branch’s latest commit.
________________________________________
🧠 2️⃣ What Happens to Uncommitted Changes?
✅ If there’s NO conflict
Your changes stay with you.
❌ If there IS a conflict
Git stops you and shows:
error: Your local changes would be overwritten by checkout.
You must:
•	Commit your changes
•	OR stash them (git stash)
•	OR discard them
________________________________________
📦 3️⃣ What Happens to the Staging Area?
The staging area (index) is also updated to match the new branch.
If staged changes would conflict, Git blocks the switch.
________________________________________
🎯 4️⃣ HEAD Moves
HEAD simply moves to point to the new branch.
Before:
HEAD → main
After:
HEAD → feature
________________________________________
📝 Simple Example
main branch:
app.js
index.html
feature branch:
app.js
index.html
style.css
Switch to feature → style.css appears
Switch back to main → style.css disappears
________________________________________
🚀 One-Line Summary
Switching branches =
Git rewrites your working directory and staging area to match the selected branch’s latest commit.
If you want, I can also explain this visually with a commit diagram to make it even clearer.

Task 2: Branching Commands — Hands-On
In your devops-git-practice repo, perform the following:
1.	List all branches in your repo
2.	Create a new branch called feature-1
3.	Switch to feature-1
4.	Create a new branch and switch to it in a single command — call it feature-2
5.	Try using git switch to move between branches — how is it different from git checkout?
6.	Make a commit on feature-1 that does not exist on main
7.	Switch back to main — verify that the commit from feature-1 is not there
8.	Delete a branch you no longer need
9.	Add all branching commands to your git-commands.md

Git Branching Practice Task
Assume you're inside your repository.
________________________________________
✅ 1️⃣ List all branches in your repo
git branch
👉 Shows local branches.
Current branch will have * next to it.
To see remote branches too:
git branch -a
________________________________________
✅ 2️⃣ Create a new branch called feature-1
git branch feature-1
This only creates the branch — it does NOT switch to it.
Verify:
git branch
________________________________________
✅ 3️⃣ Switch to feature-1
Using modern command:
git switch feature-1
Old way:
git checkout feature-1
Check current branch:
git branch
You should see:
* feature-1
________________________________________
✅ 4️⃣ Create a new branch AND switch in one command (feature-2)
Using modern way:
git switch -c feature-2
Old way:
git checkout -b feature-2
Now verify:
git branch
You should be on:
* feature-2
________________________________________
✅ 5️⃣ Move between branches using git switch
Try:
git switch feature-1
git switch main
git switch feature-2
🔎 Difference: git switch vs git checkout
git switch	git checkout
Used only for branch switching	Used for many things
Safer and clearer	Can switch branches AND restore files
Introduced in Git 2.23	Older command
👉 git switch is cleaner and less confusing.
👉 git checkout is overloaded (branch switching + file restore).
________________________________________
✅ 6️⃣ Make a commit on feature-1 that does NOT exist on main
First switch:
git switch feature-1
Create a file:
echo "This is feature-1 work" > feature1.txt
Add it:
git add feature1.txt
Commit it:
git commit -m "Add feature1.txt in feature-1 branch"
Verify:
git log --oneline
You’ll see your new commit.
________________________________________
✅ 7️⃣ Switch back to main and verify commit is not there
git switch main
Check:
ls
You should NOT see feature1.txt.
Now check log:
git log --oneline
👉 The commit you made in feature-1 will NOT appear.
💡 Why?
Because branches are separate pointers to different commit histories.
________________________________________
✅ 8️⃣ Delete a branch you no longer need
⚠️ You cannot delete the branch you're currently on.
Switch to main first:
git switch main
Delete feature-2:
git branch -d feature-2
Force delete (if not merged):
git branch -D feature-2
________________________________________
✅ 9️⃣ Add all branching commands to git-commands.md
Create or edit file:
touch git-commands.md
Add content like this:
# Git Branching Commands

## List branches
git branch
git branch -a

## Create branch
git branch feature-1

## Switch branch
git switch branch-name
git checkout branch-name

## Create and switch branch
git switch -c feature-2
git checkout -b feature-2

## Delete branch
git branch -d branch-name
git branch -D branch-name
Then commit it:
git add git-commands.md
git commit -m "Add branching commands documentation"
________________________________________

ask 3: Push to GitHub
1.	Create a new repository on GitHub (do NOT initialize it with a README)
2.	Connect your local devops-git-practice repo to the GitHub remote
3.	Push your main branch to GitHub
4.	Push feature-1 branch to GitHub
5.	Verify both branches are visible on GitHub
6.	Answer in your notes: What is the difference between origin and upstream?

Great 👍 Let’s complete this step-by-step like a real DevOps workflow.
________________________________________
✅ 1️⃣ Create a New Repository on GitHub (WITHOUT README)
1.	Go to 👉 https://github.com
2.	Click New Repository
3.	Name it: devops-git-practice
4.	Make sure:
o	❌ DO NOT check “Add a README”
o	❌ Do NOT add .gitignore
o	❌ Do NOT choose license
5.	Click Create repository
GitHub will now show you commands to push an existing repo.
________________________________________
✅ 2️⃣ Connect Local Repo to GitHub Remote
Go to your local project folder:
cd devops-git-practice
Check if remote already exists:
git remote -v
If no remote is set, add it:
git remote add origin https://github.com/<your-username>/devops-git-practice.git
Verify:
git remote -v
You should see:
origin  https://github.com/username/devops-git-practice.git (fetch)
origin  https://github.com/username/devops-git-practice.git (push)
________________________________________
✅ 3️⃣ Push main Branch to GitHub
git branch
If your branch is main, push:
git push -u origin main
-u sets upstream tracking so next time you can just use:
git push
________________________________________
✅ 4️⃣ Push feature-1 Branch to GitHub
Switch to feature-1:
git checkout feature-1
Push it:
git push -u origin feature-1
________________________________________
✅ 5️⃣ Verify Both Branches on GitHub
1.	Go to your repository on GitHub
2.	Click the Branch dropdown
3.	You should see:
o	main
o	feature-1
🎉 That means both branches are successfully pushed.
________________________________________
📝 Notes Answer
🔹 What is the difference between origin and upstream?
✅ origin
•	Default name for the remote repository you cloned from.
•	Usually your own GitHub repository.
•	When you run:
git push origin main
You are pushing to YOUR remote repo.
________________________________________
✅ upstream
•	Refers to the original repository you forked from.
•	Used in open-source contributions.
•	Example:
o	You fork a project from someone.
o	Your fork → origin
o	Original project → upstream
Example:
git remote add upstream https://github.com/original-owner/project.git
________________________________________
🔥 Simple Explanation
Term	Meaning
origin	Your remote repository
upstream	The original source repository (if forked)
________________________________________
If you want, I can now give you a real interview-style explanation of origin vs upstream for DevOps interviews 🚀

Task 4: Pull from GitHub
1.	Make a change to a file directly on GitHub (use the GitHub editor)
2.	Pull that change to your local repo
3.	Answer in your notes: What is the difference between git fetch and git pull?
________________________________________
✅ 1️⃣ Make a Change Directly on GitHub
1.	Go to your repository on GitHub
2.	Open any file (for example: README.md or any text file)
3.	Click ✏ Edit
4.	Add a new line, for example:
This change was made directly on GitHub.
5.	Scroll down → Add commit message:
Updated file from GitHub UI
6.	Click Commit changes
Now your GitHub repo has a new commit that your local repo does NOT have.
________________________________________
✅ 2️⃣ Pull That Change to Your Local Repo
Go to your local project folder:
cd devops-git-practice
Check status:
git status
Now pull the changes:
git pull origin main
Git will:
•	Contact GitHub
•	Download the new commit
•	Merge it into your local main branch
You should see something like:
Updating 4a3d2f1..8b7c6d9
Fast-forward
Now verify:
git log --oneline
You will see the commit made from GitHub.
✅ Your local repo is now synced.
________________________________________
📝 Notes Answer
🔹 What is the difference between git fetch and git pull?
✅ git fetch
•	Downloads changes from remote repository
•	DOES NOT modify your working directory
•	DOES NOT merge automatically
•	Safe to use
Example:
git fetch origin
It updates:
origin/main
But your local main branch stays unchanged.
You must merge manually:
git merge origin/main
________________________________________
✅ git pull
•	Fetches changes
•	Automatically merges into current branch
•	Updates your working directory
Example:
git pull origin main
Behind the scenes, this runs:
git fetch + git merge
________________________________________
🔥 Simple Difference Table
git fetch	git pull
Downloads changes only	Downloads + merges
Safe (no file changes)	Changes your working files
Manual merge required	Automatic merge
Good for checking updates	Good for syncing quickly
________________________________________
🎯 Interview-Style Answer
"git fetch downloads changes from the remote repository without modifying my working directory, while git pull fetches the changes and immediately merges them into my current branch."
________________________________________


Task 5: Clone vs Fork
1.	Clone any public repository from GitHub to your local machine
2.	Fork the same repository on GitHub, then clone your fork
3.	Answer in your notes:
o	What is the difference between clone and fork?
o	When would you clone vs fork?
o	After forking, how do you keep your fork in sync with the original repo?

Excellent 👌 This is very important for DevOps + open-source workflows.
I’ll give you:
1️⃣ Practical steps
2️⃣ Clear notes answers (interview ready)
________________________________________
✅ 1️⃣ Clone Any Public Repository
Example: Let’s use kubernetes official repo.
Repository:
👉 https://github.com/kubernetes/kubernetes
Clone it locally:
git clone https://github.com/kubernetes/kubernetes.git
This will:
•	Create a folder named kubernetes
•	Download full Git history
•	Set remote origin → points to original repo
Check remote:
git remote -v
You will see:
origin https://github.com/kubernetes/kubernetes.git
________________________________________
✅ 2️⃣ Fork the Same Repository
1.	Go to:
https://github.com/kubernetes/kubernetes
2.	Click Fork (top-right)
3.	Select your GitHub account
4.	GitHub creates:
https://github.com/<your-username>/kubernetes
Now you have your own copy.
________________________________________
✅ 3️⃣ Clone Your Fork
Now clone YOUR fork:
git clone https://github.com/<your-username>/kubernetes.git
Now check remote:
git remote -v
You’ll see:
origin https://github.com/<your-username>/kubernetes.git
This is your fork.
________________________________________
📝 NOTES ANSWERS
________________________________________
🔹 What is the difference between clone and fork?
✅ Clone
•	A Git command
•	Copies a repository to your local machine
•	Works locally
•	Does NOT create a copy on GitHub
Example:
git clone <repo-url>
________________________________________
✅ Fork
•	A GitHub feature
•	Creates a copy of a repository under your GitHub account
•	Used mainly for contributing to open-source projects
•	Happens on GitHub (server-side)
________________________________________
🔥 Simple Difference
Clone	Fork
Local copy	GitHub copy
Git command	GitHub feature
No new repo created online	Creates new repo under your account
Used for working locally	Used for contributing
________________________________________
🔹 When would you clone vs fork?
✅ Use Clone when:
•	You just want to use the code
•	You are part of the same team
•	You already have push access
•	You are working on your own repository
Example:
Cloning your company’s internal DevOps repo.
________________________________________
✅ Use Fork when:
•	You want to contribute to open-source
•	You do NOT have write access to original repo
•	You want your own independent copy
Example:
Contributing to kubernetes, ansible, or terraform.
________________________________________
🔹 After forking, how do you keep your fork in sync with the original repo?
This is very important 🔥
After cloning your fork:
Step 1️⃣ Add original repo as upstream
git remote add upstream https://github.com/kubernetes/kubernetes.git
Check:
git remote -v
Now you’ll see:
origin    https://github.com/<your-username>/kubernetes.git
upstream  https://github.com/kubernetes/kubernetes.git
________________________________________
Step 2️⃣ Fetch updates from upstream
git fetch upstream
________________________________________
Step 3️⃣ Merge upstream changes into your branch
git checkout main
git merge upstream/main
________________________________________
Step 4️⃣ Push updated branch to your fork
git push origin main
Now your fork is synced with the original repo.
________________________________________
🎯 Interview-Ready Answer
"Fork creates a copy of a repository under my GitHub account, while clone copies a repository to my local machine. I fork when contributing to open-source projects, and clone when I just want to work locally. After forking, I add the original repository as upstream and periodically fetch and merge upstream changes to keep my fork in sync."
________________________________________
