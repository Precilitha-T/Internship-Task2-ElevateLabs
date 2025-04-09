Jenkins CI/CD Pipeline for Application Deployment
This project demonstrates a basic CI/CD (Continuous Integration and Continuous Deployment) pipeline using Jenkins and Docker. It automates the process of building, testing, and deploying an application upon every code commit.

Objective
To set up a Jenkins pipeline that automatically builds, tests, and deploys an application using Jenkins and Docker.

Tools & Technologies

Jenkins – Automation server for CI/CD
Docker – Containerization of the application
GitHub – Source code version control
Jenkinsfile – To define the CI/CD pipeline

project-directory/

├── Jenkinsfile
├── app/ (your application code)
└── Dockerfile

Jenkinsfile Overview

The pipeline consists of the following stages:

Checkout – Pulls the latest code from GitHub

Validate - Validates the project structure and checks if all required info is available.

Compile - Compiles the source code of the application.

Test – Runs any defined test cases

Package - Packages the compiled code into a .jar or .war file.

Build – Builds a Docker image for the application

Deploy – Runs the Docker container to deploy the application

Steps to follow:

1. create an instance and Connect to that instance and execute the following commands
   sudo -i
   apt update -y && apt install default-jdk && apt install maven -y
   download jenkins
2. connect to jenkins through browser by using instance public ip address.
3. Go to configure and install docker plugins.
4. Create job using pipeline
5. Fork any application code and then give github repository link 
   pipeline code: pipeline{
    agent any
    stages{
        stage('clone'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Precilitha-T/Petclinic.git']])
            }
        }
        stage('validate'){
            steps{
                sh  'mvn validate'
            }
        }
        stage('compile'){
            steps{
                sh  'mvn compile'
            }
        }
        stage('test'){
            steps{
                sh  'mvn test'
            }
        }
        stage('package'){
            steps{
                sh  'mvn package'
            }
        }
        stage('docker image build'){
            steps{
                sh 'docker build -t vmr1 .'
                sh 'docker run --name myc2 -d -p 8083:8080 devopsvmr/vmr1 .'
            }
        }
    }
}
6. Click on Apply and save
7. Click on Build Now
8. After the build is success, copy the public ip and paste into browser with the port number and war file name

Results:
![Screenshot (231)](https://github.com/user-attachments/assets/3e739d20-952e-4d62-813a-0cea06de434a)
![Screenshot (233)](https://github.com/user-attachments/assets/73a712f3-a7fa-430a-8ade-f0718ad5bfb7)
![Screenshot (232)](https://github.com/user-attachments/assets/fe2f4c52-c775-4b44-a4e4-40e35ea03da8)



