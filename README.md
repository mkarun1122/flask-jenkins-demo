
🧪 DevOps Laboratory Experiment
Experiment Title:
CI/CD Pipeline Setup using Jenkins for a Python Flask Application on Windows
________________________________________
🎯 Objective
To understand and implement Continuous Integration (CI) and Continuous Deployment (CD) for a Python Flask web application using Jenkins on a Windows platform.
________________________________________
🧰 Software and Tools Required
Tool	Description
Windows 10/11	Operating System
Python 3.10+	Programming Language
Flask	Python Web Framework
pip	Python Package Manager
Git	Version Control System
Jenkins	Automation Server for CI/CD
Web Browser	To access Jenkins Dashboard
(Optional) Docker	For containerized deployment
________________________________________
________________________________________
🧱 Experiment Procedure
Step 1: Install Python and Flask
1.	Download and install Python from https://www.python.org/downloads.
2.	Verify installation:
3.	python --version
4.	Install Flask:
5.	pip install flask
6.	Create a simple Flask app app.py:
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, Jenkins CI/CD with Flask!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
________________________________________
Step 2: Initialize Git Repository
1.	Create a new folder and initialize Git:
2.	git init
3.	Add files and commit:
4.	git add .
5.	git commit -m "Initial Flask app"
6.	Push to a GitHub repository:
7.	git remote add origin https://github.com/<your-username>/flask-jenkins-demo.git
8.	git push -u origin main
________________________________________
Step 3: Install and Configure Jenkins
1.	Download Jenkins for Windows from https://www.jenkins.io/download.
2.	Run the installer and complete the setup.
3.	Access Jenkins at http://localhost:8080.
4.	Unlock Jenkins using the password from:
5.	C:\Program Files\Jenkins\secrets\initialAdminPassword
6.	Install suggested plugins and create an admin user.
________________________________________
Step 4: Configure Jenkins for Python
1.	Open Jenkins → Manage Jenkins → Global Tool Configuration.
2.	Add Python installation path (e.g., C:\Python311\python.exe).
3.	Install the Git plugin if not already installed.
________________________________________
Step 5: Create Jenkins Job (Freestyle or Pipeline)
Option 1: Freestyle Project
1.	Create a New Item → Freestyle project.
2.	Under Source Code Management, choose Git and enter your GitHub repo URL.
3.	Under Build Triggers, enable:
o	✅ “Poll SCM” or
o	✅ “GitHub hook trigger for GITScm polling”
4.	Under Build Steps, add a Windows batch command:
5.	pip install -r requirements.txt
6.	python -m unittest discover
7.	python app.py
________________________________________
Option 2: Jenkins Pipeline using Jenkinsfile
Create a file named Jenkinsfile in your repository:
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/<your-username>/flask-jenkins-demo.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'python -m unittest discover'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Starting Flask App...'
                bat 'python app.py'
            }
        }
    }
}
________________________________________
Step 6: Test CI/CD Workflow
1.	Push code changes to GitHub.
2.	Jenkins automatically triggers a build.
3.	Observe console output:
o	Dependencies installed
o	Tests executed
o	Flask app deployed
________________________________________
Step 7: Access Application
•	Flask app runs on http://localhost:5000.
•	Jenkins displays build logs and build history.
________________________________________
📊 Observation / Output
•	Jenkins automatically detects code changes from GitHub.
•	Flask application is built, tested, and deployed automatically.
•	The output “Hello, Jenkins CI/CD with Flask!” is displayed on the browser.
________________________________________
📘 Result
Successfully implemented CI/CD pipeline using Jenkins for a Python Flask application on Windows.
The process automated build, test, and deployment stages of the DevOps lifecycle.






Initialize Git Repository
------------------------


Github url:

https://github.com/mkarun1122/flask-jenkins-demo#

PS D:\NRCM\DevOpsLab\JenkinsDemo1> git init 
Initialized empty Git repository in D:/NRCM/DevOpsLab/JenkinsDemo1/.git/
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git add .
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git commit -m "Initial Flask app"      
[master (root-commit) b9bbc47] Initial Flask app
 1 file changed, 9 insertions(+)
 create mode 100644 app.py
PS D:\NRCM\DevOpsLab\JenkinsDemo1>  git remote add origin git@github.com:mkarun1122/flask-jenkins-demo.git
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git push -u origin main      
error: src refspec main does not match any
error: failed to push some refs to 'github.com:mkarun1122/flask-jenkins-demo.git'
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git branch -M main
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git push -u origin main
To github.com:mkarun1122/flask-jenkins-demo.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'github.com:mkarun1122/flask-jenkins-demo.git'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 5 (delta 0), reused 5 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (5/5), 515 bytes | 11.00 KiB/s, done.
From github.com:mkarun1122/flask-jenkins-demo
 * [new branch]      main       -> origin/main
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> main

 ! [rejected]

PS D:\NRCM\DevOpsLab\JenkinsDemo1> git push -u origin main
To github.com:mkarun1122/flask-jenkins-demo.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'github.com:mkarun1122/flask-jenkins-demo.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

REBASE

PS D:\NRCM\DevOpsLab\JenkinsDemo1> git pull origin main --rebase
From github.com:mkarun1122/flask-jenkins-demo
 * branch            main       -> FETCH_HEAD
warning: skipped previously applied commit b9bbc47
hint: use --reapply-cherry-picks to include skipped commits
hint: Disable this message with "git config set advice.skippedCherryPicks false"
Successfully rebased and updated refs/heads/main.
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git push origin main
Everything up-to-date
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        app.py

nothing added to commit but untracked files present (use "git add" to track)
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git add .
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git commit -m " First flask file"
[main f53108d]  First flask file
 1 file changed, 9 insertions(+)
 create mode 100644 app.py
PS D:\NRCM\DevOpsLab\JenkinsDemo1> git push
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 395 bytes | 395.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To github.com:mkarun1122/flask-jenkins-demo.git
   0525752..f53108d  main -> main
PS D:\NRCM\DevOpsLab\JenkinsDemo1> 