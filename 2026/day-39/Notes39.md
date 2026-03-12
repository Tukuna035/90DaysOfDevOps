Day 39 – What is CI/CD?

Task 1: The Problem
Think about a team of 5 developers all pushing code to the same repo manually deploying to production.
Write in your notes:
1.	What can go wrong?
2.	What does "it works on my machine" mean and why is it a real problem?
3.	How many times a day can a team safely deploy manually?
………………………………………………………………………………………………………………….

1. What can go wrong when 5 developers manually deploy to production?
Many problems can happen:
1. Conflicting code
•	Two developers may deploy different versions of the code.
•	One deployment may overwrite another.
2. Wrong version deployed
•	Someone may deploy old code instead of the latest code.
3. Human mistakes
•	Forgetting steps in the deployment process.
•	Running commands in the wrong order.
•	Deploying to the wrong server.
4. No consistency
•	Each developer may follow slightly different deployment steps.
5. Downtime
•	If something breaks during deployment, the application may go down.
6. Hard to track changes
•	No clear record of who deployed what and when.
________________________________________
2. What does “It works on my machine” mean?
“It works on my machine” means:
A developer’s code runs correctly on their local computer, but fails on another developer’s machine or in production.
Example reasons:
•	Different Node/Python/Java versions
•	Missing dependencies
•	Different OS
•	Different environment variables
•	Different database versions
Example scenario:
•	Developer A uses Node 18
•	Production server uses Node 16
•	The code works locally but fails in production
________________________________________
3. Why is this a real problem?
Because it causes:
•	Production failures
•	Debugging difficulty
•	Wasted time
•	Unpredictable releases
Teams may spend hours figuring out why something works locally but not in production.
This is why DevOps uses tools like:
•	Docker → same environment everywhere
•	CI/CD pipelines → automated testing and deployment
________________________________________
4. How many times a day can a team safely deploy manually?
Usually very few times.
Typical manual deployments:
•	1–2 deployments per day
•	Sometimes only once per week
Reason:
•	Manual deployments are slow and risky.
With CI/CD automation, teams like big tech companies can deploy:
•	10–100+ times per day
________________________________________
✅ Summary
Problem	Result
Manual deployments	Human errors
Different environments	“Works on my machine” problem
No automation	Slow and risky releases
Multiple developers deploying	Conflicts and instability
________________________________________
If you want, I can also explain how CI/CD solves all these problems step-by-step, which is usually the next topic after GitHub in DevOps learning.

Task 2: CI vs CD
Research and write short definitions (2-3 lines each):
1.	Continuous Integration — what happens, how often, what it catches
2.	Continuous Delivery — how it's different from CI, what "delivery" means
3.	Continuous Deployment — how it differs from Delivery, when teams use it
Write one real-world example for each.
…………………………………………………………………………………………………………………………..
1. Continuous Integration (CI)
Definition:
Continuous Integration is a development practice where developers frequently merge their code into a shared repository, often several times a day. Each commit automatically triggers builds and automated tests to detect integration issues early.
What it catches:
•	Code conflicts
•	Build failures
•	Failing tests
Real-world example:
A team uses GitHub Actions to automatically run tests every time code is pushed to GitHub. If the tests fail, the merge is blocked.
________________________________________
2. Continuous Delivery (CD)
Definition:
Continuous Delivery is an extension of CI where code changes that pass all tests are automatically prepared for release to production, but the final deployment step requires manual approval.
What "delivery" means:
The application is always ready to be deployed, but a human decides when to release it.
Real-world example:
A company uses Jenkins to automatically build and test the application, then create a deployable package. A release manager manually deploys it to production when ready.
________________________________________
3. Continuous Deployment
Definition:
Continuous Deployment goes one step further than Continuous Delivery. After passing all tests, code changes are automatically deployed to production without human intervention.
When teams use it:
•	When they have very strong automated testing
•	When they want very fast releases
Real-world example:
Companies like Netflix automatically deploy code changes using automated pipelines and monitoring systems to ensure the new version works correctly.
________________________________________
✅ Quick Comparison
Practice	Deployment to Production	Human Approval
Continuous Integration	No	Not applicable
Continuous Delivery	Ready for deployment	Yes
Continuous Deployment	Automatic	No


Task 3: Pipeline Anatomy
A pipeline has these parts — write what each one does:
•	Trigger — what starts the pipeline
•	Stage — a logical phase (build, test, deploy)
•	Job — a unit of work inside a stage
•	Step — a single command or action inside a job
•	Runner — the machine that executes the job
•	Artifact — output produced by a job
………………………………………………………………………………………………………………………
Here are short definitions (2–3 lines each) for the CI/CD pipeline terms.
1. Trigger
A trigger is the event that starts a CI/CD pipeline.
Common triggers include code pushes, pull requests, scheduled jobs, or manual runs.
Example: Pushing code to a repository in GitHub automatically starts a pipeline.
________________________________________
2. Stage
A stage is a logical phase in the pipeline that groups related jobs.
Typical stages include build, test, and deploy, and they run in sequence.
________________________________________
3. Job
A job is a unit of work inside a stage.
Each job runs a set of steps on a runner and performs a specific task such as building code or running tests.
________________________________________
4. Step
A step is a single command or action inside a job.
Examples include running a shell command, installing dependencies, or executing a test script.
________________________________________
5. Runner
A runner is the machine (virtual machine, container, or server) that executes the pipeline jobs.
For example, a runner provided by GitHub Actions executes the build and test tasks defined in a workflow.
________________________________________
6. Artifact
An artifact is a file or output produced by a job that is saved for later stages.
Examples include compiled binaries, build packages, Docker images, or test reports.
________________________________________
✅ Simple Flow Example
Trigger → Stage (Build) → Job → Steps → Runner executes → Artifact produced
________________________________________
If you want, I can also show a simple real CI/CD pipeline example (GitHub Actions YAML) where you can clearly see trigger, stages, jobs, steps, runner, and artifacts in one file.

Task 4: Draw a Pipeline
Draw a CI/CD pipeline for this scenario:
A developer pushes code to GitHub. The app is tested, built into a Docker image, and deployed to a staging server.
Include at least 3 stages. Hand-drawn and photographed is perfectly fine.
………………………………………………………………………………………………………………………………………………

You can draw a simple CI/CD pipeline diagram like this for your notes. It should show the flow from code push → testing → build → deployment.
Example CI/CD Pipeline Diagram
Developer
   │
   │  (Push Code)
   ▼
GitHub Repository
   │
   │  Trigger Pipeline
   ▼
┌───────────────┐
│   Stage 1     │
│     TEST      │
│ Run unit tests│
└───────────────┘
        │
        ▼
┌───────────────────┐
│     Stage 2       │
│      BUILD        │
│ Build Docker Image│
└───────────────────┘
        │
        ▼
┌───────────────────┐
│     Stage 3       │
│      DEPLOY       │
│ Deploy to Staging │
│ Server            │
└───────────────────┘
        │
        ▼
   Staging Environment
What each stage does
1. Test Stage
•	Runs automated tests (unit tests, lint checks).
•	Stops pipeline if tests fail.
2. Build Stage
•	Builds the application.
•	Creates a Docker image.
3. Deploy Stage
•	Pushes the Docker image.
•	Deploys the application to a staging server for testing.
Technologies commonly used
•	Code repo: GitHub
•	CI/CD pipeline: GitHub Actions or Jenkins
•	Containerization: Docker
✅ Tip for your assignment:
You can draw this on paper as:
Developer → GitHub → TEST → BUILD (Docker Image) → DEPLOY → Staging Server
Add boxes for stages and arrows for flow, then take a photo.
________________________________________
If you want, I can also show you a very clean DevOps interview-style CI/CD pipeline diagram that many companies expect candidates to understand.

Task 5: Explore in the Wild
1.	Open any popular open-source repo on GitHub (Kubernetes, React, FastAPI — pick one you know)
2.	Find their .github/workflows/ folder
3.	Open one workflow YAML file
4.	Write in your notes:
o	What triggers it?
o	How many jobs does it have?
o	What does it do? (best guess)
………………………………………………………………………………………………………………………………………………
