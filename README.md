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

gradle execute sequence:

 $ mkdir myproject
 $ cd myproject
 $ gradle init -> generates bare minimum files 
 $ vi build.gradle 

    task sayHello {
        println 'Hello, World!'
    }

    task anotherTask << {
        println 'This is another task'
    }

    sayHello.dependsOn anotherTask

 $ ./gradlew sayHello
 $ ./gradlew anotherTask
 $ ./gradlew anotherTask satHello
 $ ./gradlew nodeSetup


```
```

- Automated Testing 
    What is Automated Testing ? 
        - Automated testing is the automated execution of tests that verify the quality and stability of code. 
        - Automated tests are usually code themselves, so they are code that is written to test other code. 
        - Automated tests are often run as part of the build process and are executed using build tools like Gradle.

- Types of Automated Tests
    There arfe multiple types of automated tests: 
        - Unit Tests - focus on testing small pieces of code is isolation, Usually a single method or function. 
        - Integration Tests - test larger portion of an application that are integrated with each other. 
        - Smoke Tests/Sanity Tests - these are high-level integration test that are very basic, large-scale things like whether or not the application runs, whether application enpoints return http 500 errors etc. 

- Running Automated Tests in Gradle:
    How the tests are run depends on what type of tests you have and the technology used to build them. Generally, automated tests will be run in Gradle as a task that gets executed as part of the build process:
        - task build
        - task test
        - build.dependsOn test
        - https://github.com/linuxacademy/cicd-pipeline-train-schedule-gradle (solution branch)

        $ ./gradlew npm_test
- QUIZ: Build Automation

*************************************************
- Hands-On: Creating Build Automation with Gradle
*************************************************
***************************************
- Creating Build Automation with Gradle
***************************************
Creating Build Automation with Gradle
Introduction
Build Automation is an important part of continuous integration, and a necessary component of many automated pipelines. Gradle is a powerful build automation tool. In this lab, we'll step through the process of implementing a basic Gradle build. When we're finished, we'll have a good working knowledge build automation basics in Gradle.

Prerequisites
For this lab, we'll need a GitHub account set up and ready to go. That's about it as far as things we need ahead of time. Let's see what we've got ahead of us

The Scenario
Developers have created the first prototype of a train scheduling app. They need us to create a Gradle build for it. The developers need this build to execute some automated tests that they have written. If the automated tests pass, the build needs to produce a packaged archive that includes the application code and its dependencies. The completed archive should be located in the project folder as dist/trainSchedule.zip.

In short, this automation needs to:

Have a build task that can be called to execute the entire build process
Execute some automated tests (where any testing failures cause the build to fail)
Package the code and its dependencies into a zip archive called dist/trainSchedule.zip
A List of Steps
In order to accomplish this, you will need to perform several steps. We'll number them here, and follow this outline through the lab.

Configure git for ssh authentication with GitHub.com
Create a personal fork of the sample repository https://github.com/linuxacademy/cicd-pipeline-train-schedule-gradle
Clone your personal fork from GitHub
Initialize the project with Gradle
Create a Gradle build task
Include the com.moowork.node plugin in the Gradle project
Execute automated tests as part of the build with the npm_test task
Create a task to generate a zip archive (dist/trainSchedule.zip) of the files that need to be depoyed to production
Make sure task dependencies are set up so tasks execute in the correct order
Commit and push these changes to your GitHub fork
Configure git for ssh Authentication with GitHub.com
Once we're logged into the server, we'll find that Git is already installed. It's not configured though, so we'll have to do that before we can go any further. We'll have to run a few git config commands:

[cloud_user@$host]$ git config --global user.name "Our Name"
[cloud_user@$host]$ git config --global user.email "ourname@ourdomain.com"
[cloud_user@$host]$ ssh-keygen -t rsa -b 4096
[cloud_user@$host]$ cat /home/cloud_user/.ssh/id_rsa.pub
Now, over on https://github.com, we can get into our account, in Settings, and go to the SSH and GPG keys in the left-hand menu of our profile page. Let's click on the green New SSH key button, give it a Title of something simple (Like gradle activity). In the Key area, paste in the contents of /home/cloud_user/.ssh/id_rsa.pub, which should still be open in a terminal somewhere with the output of that cat command we ran.

Create a Personal Fork of the Sample Repository
The project is sitting up on GitHub, at https://github.com/linuxacademy/cicd-pipeline-train-schedule-gradle. Let's head over there, and click on Fork. When prompted for where to fork this to, pick your own Git repository. Then we'll be dumped into our own https://github.com/ourname/cicd-pipeline-train-schedule-gradle, where ourname is our own username.

Clone Our Personal Fork from GitHub
To clone this, we need to click the Clone or download button. We'll get a little Clone with SSH dropdown with a string (git@github.com...) that we need to copy. Back over in our terminal, let's make sure we're in our home directory with a , then paste that string into a git clone command (remembering that ourname needs to be our actual GitHub username):

[cloud_user@$host]$ cd ~/
[cloud_user@$host]$ git clone git@github.com:ourname/cicd-pipeline-train-schedule-gradle.git
If we've never grabbed anything from GitHub before, we'll be prompted with something about "The authenticity of host...". Just type yes and keep going. We should see the repository copy down to our server.

Initialize the Project with Gradle
Once we have the Git repository cloned to our home directory, let's cd into the directory and initialize the Gradle build. We'll check afterward with an ls to see if we've got all the source code:

[cloud_user@$host]$ cd ~/cicd-pipeline-train-schedule-gradle
[cloud_user@$host]$ ./gradlew init
[cloud_user@$host]$ ls -la
Create a Gradle Build
We have to create a Gradle build, but before that we have to install Gradle itself. That won't be too difficult though, because there's a Gradle wrapper included in the repository. This is essentially a collection of scripts that will install Gradle all by itself. As long as we have Java 7 or later installed, we're good to go. This will make it much easier to install Gradle and run the build of our train scheduling app. There's a file in this repository called gradlew, and that is what we'll use to install Gradle and run gradle commands. To get that process moving, let's build Gradle by executing that script:

[cloud_user@$host]$ ./gradlew build
When we run it, we'll see that it's actually installing Gradle. That will only happen this first time though, because Gradle isn't currently installed on our system. The script doesn't do much else, because we haven't actually set up the build yet.

The next thing we have to do is to initialize the Gradle build:

[cloud_user@$host]$ ./gradlew init
If we check with another ls -la command, we'll now see a build.gradle file that wasn't there before. We're going to edit that file (with whatever text editor you prefer -- vi, nano, emacs, etc) and delete what's in there now. The current text is just a comment anyway, so we don't need it. When we're done, the file should look like this (here with comments to explain things, then below that just the required lines):

With comments

// This application is built in node.js, and there is a plugin for it in Gradle that does
// a lot of the work for us as far as dealing with node.js builds. We're calling in that
// plugin here
plugins {
  id "com.moowork.node" version "1.2.0"
}

// We've also got to confgure the plugin a little bit. This line will instruct the node plugin
// to download and install node.js and npm locally, for this particular project. It ensures that
// those are installed during the build, but not system-wide, just within this directory.
node {
  download = true
}

// Whenever we call the build task (it's a task called build) which will run any and all
// other tasks that are required to actually call the build "built."
task build

// All we need to do, in order for this build to actually run, is to call some of the tasks
// built in to the node.js and npm plugins. We're going to call them here.
build.dependsOn npm_build
Without comments:

plugins {
  id "com.moowork.node" version "1.2.0"
}

node {
  download = true
}

task build

build.dependsOn npm_build
Save that file out, and we can build again.

Create the Gradle Build Again
We're going to build again, but this time including all of the things we just put in gradle.build. Gradle won't be downloaded again, because we got it the first time we ran build. Run the same command as before:

[cloud_user@$host]$ ./gradlew build
This time we'll see the node plugin getting downloaded though. We should land back at a command prompt, after a successful build.

Now let's edit build.gradle again. We've got to tack something on to the end of the file.

...
npm_build.dependsOn npmInstall
This will ensure that we run npmInstall. It ensures that we download any shared library dependencies that this particular node.js application requires.

Just like our we set our build to depend on npm_build in the line before this new one, we're going to make our npm.build depend on npmInstall. If npmInstall fails, then our npm.build will fail, and that will cause our build to fail.

Now let's run the build again:

[cloud_user@$host]$ ./gradlew build
Notice this time that there's no node getting downloaded, since it happened during our last build, but this time we're downloading npmInstall. This may take some time (several minutes) so be patient.

If we run the same build again, we'll see that it's finished in just a couple of seconds. Gradle is very good at detecting when build steps don't need to be run again, and doesn't perform them when it doesn't need to.

Execute Automated Tests as Part of the Build with the npm_test Task
We want to ensure that our build runs our automated tests. These are simple things, like sanity tests that confirm whether or not the application will start up and respond to requests. We're going to add another couple of lines at the bottom of our build.gradle file to do this:

...
npm_build.dependsOn npm_test
npm_test.dependsOn npmInstall
The first sets up those tests. The second though makes sure that npm_test depends on npmInstall. Since Gradle is capable of running tasks in parallel (two or more tasks at the same time), we need to set up these dependencies to run in a specific order. We want to make sure that npmInstall is finished before npm_test starts up, and we want to make sure npm_test is done before npm_build happens. Now if we run the build again, we'll get some output related to the testing. We should see that GET / and GET /trains both run successfully, showing us a 2 passing (XXXms) line near the end of the build command's output.

The way things work now, the automated tests get run as part of the build. If we (or developers) make a code change that causes one of these tests to fail, the build itself will fail. And we'll get immediate feedback, letting us know that we broke something.

Create a Task to Generate a zip Archive of the Files that Need to be Deployed to Production
We need to create a single zip file containing all of the source code. Deploying the code will then a simple matter of unzipping the archive. The Gradle build should generate an archive of the application in dist/trainSchedule.zip.

Gradle comes with some built-in functionality to facilitate this. We've just got to add a task that utilizes it in order to create this archive. Between task build and build.dependsOn npm_build, we're going to write this zipping task: With Comments

plugins {
 id "com.moowork.node" version "1.2.0" 
}

node {
 download = true
}

task build

task zip(type: Zip) {
    from ('.') {
        include "*"
        include "bin/**"
        include "data/**"
        include "node_modules/**"
        include "public/**"
        include "routes/**"
        include "views/**"
    }
    destinationDir(file("dist"))
    baseName "trainSchedule"
}

build.dependsOn zip
zip.dependsOn npm_build
build.dependsOn npm_build
npm_build.dependsOn npmInstall
npm_build.dependsOn npm_test
npm_test.dependsOn npmInstall




Tools
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
