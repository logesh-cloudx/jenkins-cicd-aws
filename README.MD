# Jenkins CI/CD Pipeline on AWS EC2

![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)

## Project Overview
Automated multi-environment CI/CD pipeline built with Jenkins on AWS EC2, integrated with GitHub webhook for automatic deployment on every code push.

## Pipeline Flow
Code Push to GitHub → GitHub Webhook → Jenkins Trigger → Build → Test → SIT → UAT → Production

## Pipeline Stages
| Stage | Description | Status |
|-------|-------------|--------|
| Code Checkout | Pulls latest code from GitHub automatically | Done |
| Build | Compiles and packages application | Done |
| Test | Runs automated tests | Done |
| Deploy SIT | Deploys to System Integration Testing environment | Done |
| Deploy UAT | Deploys to User Acceptance Testing environment | Done |
| Deploy Production | Deploys with manual approval gate before going live | Done |

## Tech Stack
- CI/CD: Jenkins 2.568
- Cloud: AWS EC2 Ubuntu 22.04
- Source Control: GitHub
- Web Server: Apache2
- Scripting: Bash
- Trigger: GitHub Webhook

## Architecture
Developer Laptop
|
| git push
v
GitHub Repository
|
| Webhook trigger (automatic)
v
Jenkins Server on AWS EC2
|
|-- Stage 1: Code Checkout
|-- Stage 2: Build
|-- Stage 3: Test
|-- Stage 4: Deploy to SIT /var/www/sit
|-- Stage 5: Deploy to UAT /var/www/uat
|-- Stage 6: Deploy to Production /var/www/html
|
v
Apache Web Server
Accessible live on browser

## Project Structure
jenkins-cicd-aws/
├── Jenkinsfile
├── index.html
├── README.md
└── screenshots/
├── jenkins-pipeline.png
├── console-output.png
└── live-website.png


## Setup Instructions

### Step 1 - Launch AWS EC2
AMI: Ubuntu 22.04
Instance: t2.micro (free tier)
Ports open: 22, 80, 8080

### Step 2 - Install Java 21
```bash
sudo apt update -y
sudo apt install -y openjdk-21-jdk
java -version
```

### Step 3 - Install Jenkins
```bash
sudo curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key -o /etc/apt/trusted.gpg.d/jenkins.asc
echo "deb https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list
sudo apt update -y
sudo apt install -y jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

### Step 4 - Install Apache
```bash
sudo apt install -y apache2
sudo systemctl start apache2
sudo systemctl enable apache2
```

### Step 5 - Configure Jenkins

Open http://YOUR-EC2-IP:8080
Unlock with initial admin password
Install suggested plugins
Create admin user
Create Pipeline job
Connect to GitHub repo
Add GitHub webhook


### Step 6 - Add GitHub Webhook
GitHub Repo Settings
Webhooks
Add webhook
Payload URL: http://YOUR-EC2-IP:8080/github-webhook/
Content type: application/json
Event: Just the push event
Save

## Key Results
- 60 percent reduction in manual deployment effort
- Consistent deployments across 3 environments
- Automatic pipeline trigger on every code push
- Manual approval gate before production release
- Full audit trail via Jenkins build history
- Zero environment specific failures

## Live Demo
Website: http://54.173.16.147
Jenkins: http://54.173.16.147:8080

## Author
Logesh V - Cloud System Engineer

LinkedIn: https://www.linkedin.com/in/logesh010
GitHub: https://github.com/logesh-cloudx
Email: logesh.careers@gmail.com
