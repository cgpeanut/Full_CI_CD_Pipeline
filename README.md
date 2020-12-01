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

- Here's the commands to install the Gradle wrapper: 
$ cd ~/
$ mkdir my-project
$ cd my-project
$ gradle wrapper
$ ./gradlew build

- The Gradle Wrapper:
    - One of the features of Gradle that we will use is the Graddle Wrapper which is a script that invokes a declared version of Gradle. downloading it beforehand if necessary.
    - Graddle Wrapper allows Gradle to install using the files from your project's source control.
- The Wrapper is usefull becuause:
    - It removes the need to have Gradle installed beforehand in order to run the build.
    - Ensures the project is always build with a specific version of Gradle.
    - Let's you build multiple projects with different Gradle version in one system.
    - Anyone (or any automated process) can run the build quickly and easily - They only need Java

Installing The Gradle Wrapper explanation:
If you already have a normal Gradle install on your system, you can use it to easily install the wrapper:
    - $ cd /your/project/root/directory
    - $ gradle wrapper
You should also add the gradle to you .gitignore file.

This will place a script file in your project's root directory called gradlew (there's also a gradlew.bat for windows systems).
    - cd /your/project/root/directory
    - ./gradlew build

- Gradle Basics
    A gradle build is defined in a groovy script called "build gradle", located in the root directory of your project. 
    Use "gradle init" to initialize a new project. This also sets up a gradle warpper for you.

- Running a Gradle Build:

Gradle builds consists a set of tasks that you call from the command line. 
    - ./gradlew someTask someOtherTask
This command will run a task named soimeTask, and a task named someOtherTask.

- Defining Tasks

The "build gradle" file controls what tasks are available for you project.

You can define your own task with custom code in "build gradle":
    task myTask{
        println "Hello, World!"
    }
Most of the tasks you use will come built into other Gradle itself or plugins

- Task Dependencies:
Gradle uses the concept of task dependencies to determinewhat tasks need to be run for a particular build command:
    - if you run a task, any other tasks that depend on it will also be run.

Task dependencies also determine the order in which tasks get run:
    - A Task's dependencies will always run before that tasks

You can define a dependency relationship between tasks in "build gradle" like this:
    - taskA.dependsOn taskB

- Plugins:
    Gradle has a huge variety of plugins available, many of them contributed by the community.

    Plugins add all kinds of functionality to Gradle. The usually include pre-built tasks that you can configure to do what you need.

    You can include plugins in your "build gradle" like this:
        plugins {
            id "<plugin id>" version "<plugin version>"
        }

    public opensource plugins located at: https://plugins.gradle.org/

Gradle is a powerful build automation tool, but in order to use it you need to know the basics of how it works. This lesson will
guide you through the core concepts of Gradle automation, and it will demonstrate creating a simple build.gradle file. After
completing this lesson, you should have a basic working knowledge of how to implement and execute tasks in Gradle.
More more information on Gradle, check out the official Gradle site: https://gradle.org
Here is the final build.gradle from the demo:

    plugins {
        id 'com.moowork.node' version '1.2.0'
    }

    task sayHello {
        doLast {
        println 'Hello, World!'
        }
    }

    task anotherTask {
        doLast {
        println 'This is another task'
        }
    }


If you have the gradle wrapper installed in your project (for example, by using gradle init), you can run the build defined in this
build.gradle like so:

 $ ./gradlew sayHello






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
