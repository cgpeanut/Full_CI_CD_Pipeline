# Full_CI_CD_Pipeline
Chapter 1: Implementing a Full CI/CD Pipeline

Guide you through the process of building a CI/CD Pipeline using a viriety of tools.  It Begins with basic CI-related concepts, like source control and build automation. Then it moves along to copvering containers,
orchestration, and monitoring.  Finally, the course covers how to strengthen the stability of yor pipeline
using things like self-healing and autoscaling, and canary deployments. 

This course focuses on using a variety of tools and how they fit together as part of the CI/CD pipeline "Big Picture".
```
The Big Picture: 
- gives you a hands-on introduction to some of the techniques and tools involved in doing CI/CD.
- gives you an ide of what implementing CI/CD can look like in practice.
- provides enough knowledge to decide what you many wan tot learn more about. 
- shows you technologies and tools thatyou can use to implement CI and CD directly, like CI tools and automated deployment techniques. 
- shows you infrastructure tools that are desgned to provide stability in the context of CD.
  - Jenkins    - CI/CD
  - Git        - Source Control Management
  - Gradle     - Build Automation
  - Docker     - Containerization
  - Kubernetes - Orchestration and Stability 
  - Permetheus/Grafana - Monitoring Tools
```
```
Chapter 2: Source Management 
- Introduction to SCM
    - Source Control Management (SCM) is an important component of our CI/CD Pipeline. 
        - It's a huge part of daily dev workflow
            - all code changes made by devs will need to be tracked in SCM
            - Devs will use SCM to track their chjanges separately and then merge them together
        - All pieces of automation that need to interact with the source code will use SCM:
            - Continuos Integration(CI) will get the code from SCM
            - SCM will notify the cI server when code needs to be built
    - Understanding Git-based workflow
    - Steps involved in order to make changes to the source code and ensure that the change is managed by Git:
            - cloning
            - adding 
            - commiting 
            - pushing
            - branching 
            - merging 
            - pull requests

- Installing Git
    - We'll use Git specifically GitHub to manage source code for the Train Schedule app.
- Creating GitHub Forks
- Making changes in Gitto
- Branches and Tags
- Pull Requests
- QUIZ: Source Code Management 
- Hands-On: Use Git to make changes to Code
```
```
Chapter 3: Build Automation
- Introduction to Build Automation
    Build Automation: is the automation of tasks needed in order to process and prepare source code for deployment to production. It is an importmant component of continuous integration.
    This includes things like:
        - compiling 
        - dependency management 
        - executing automated tests
        - packaging app for deployment

- Installing Gradle and Gradle Wrapper - after which will allow us to create gradle builds.

$ cd ~/
$ wget -O ~/gradle-4.7-bin.zip https://services.gradle.org/distributions/gradle-4.7-bin.zip
$ sudo yum -y install unzip java-1.8.0-openjdk
$ sudo mkdir /opt/gradle
$ sudo unzip -d /opt/gradle/ ~/gradle-4.7-bin.zip
$ sudo vi /etc/profile.d/gradle.s

- Put this text into gradle.sh:

$ export PATH=$PATH:/opt/gradle/gradle-4.7/bin

- Then set permissions on gradle.sh:

$ sudo chmod 755 /etc/profile.d/gradle.sh

- Validate:  

$ gradle --version

- Here;s the commands to install the Gradle wrapper: 
$ cd ~/
$ mkdir my-project
$ cd my-project
$ gradle wrapper
$ ./gradlew build


- Gradle Basics
- Automated Testing 
- QUIZ: Build Automation
- Hands-On: Creating Build Automation with Gradle
```
```
Chapter 4: Continous Integration
- Ci Overview
- Installing Jenkins
- Setting up Jenkins Projects
- Triggering Git with Git Hooks
- QUIZ: Continous Integration
- Hands-On: Building an App as a Frestyle Jenkins Project
```
```
Chapter 5: Continous Delivery
- Introducing Jenkins Pipelines
- Jekins Pipeline Stages and Steps
- Deployment with Jenkins Pipelines
- QUIZ: Continous Delivery
- Hands-On: Building a Jenkins Pipeline
- Hands-On: Implementing Automated Deployment Through a Jenkins Pipeline
  Chapter 6: Containers
- Why Containers?
- Installing Docker
```
```
Chapter 6: Containers
- Why Containers ?
- Installing Docker
- Docker Basics
- Building a Dockerfile
- Running Docker in Production
- Installing Docker on Jenkins
- Jenkins Pipelines CD and a Dockerized App
- Hands-On: Dockerizing an App
- Hands-On: Deploying a Container with Jenkins Pipelines
```
```
Chapter 7: Orchestration
- Orchestration
- Creating a Kubernetes Cluster
- Kubernetes Basics
- Deploying to Kubernetes with Jenkins
- Hands-On: Deploying Kubernetes with Jenkins Pipelines
```
```
Chapter 8: Monitoring 
- Monitoring
- Installing Prometheus and Grafana
- Cluster Monitoring
- Application Monitoring
- Alerting
- Hands-On: Monitoring Kubernetes with Prometheus and Grafana
```
```
Chapter 9: Self Healing
- Kubernetes and Self Healing
- creating Liveness Probes in Kubernetes
- Hands-On: Setting up Self-Healing Apps in Kubernetes
```
```
Chapter 10: Autoscaling
- Kubernetes and Autoscaling 
- Horizontal Pod Autoscalers in Kubernetes
- Hands-On: Autoscaling in Kubernetes
```
```
Chapter 11: Canary Testing 
- What is Canary Testing ?
- Implementing a Canary Test in Kubernetes
- Kubernetes Canary Testing with Jenkins Pipelines 
- Hands-On: Canary Deployments with Kubernetes and Jenkins
```
```
Chapter 12: Fully-Automated Deployment 
- Fully Automated Deployment 
- Hands-On: implementing Fully-Automated Deployment in a CD Pipeline
```
```
Chapter 13: Next Steps
Nest Steps
```
```
```
