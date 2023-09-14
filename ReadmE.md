# CI/CD Pipeline for Node.js Application using Jenkins, GitHub, AWS and Docker

Welcome to the comprehensive guide on creating a CI/CD pipeline for your Node.js application using Jenkins, GitHub, and Docker. This README provides detailed step-by-step instructions to ensure a seamless setup process.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setting Up](#setting-up)
   1. [Creating an EC2 Instance](#creating-an-ec2-instance)
   2. [Installing Jenkins](#installing-jenkins)
   3. [Jenkins Setup](#jenkins-setup)
   4. [Generating SSH Keys](#generating-ssh-keys)
   5. [Integrating GitHub and Jenkins](#integrating-github-and-jenkins)
   6. [Automating Docker Build and Run](#automating-docker-build-and-run)
   7. [Automate Docker Build and Run with Jenkins](#automation-through-jenkins)
3. [Conclusion](#conclusion)

## Prerequisites

- AWS account for creating an EC2 instance.
- Basic familiarity with the command line interface.
- Basic familiarity with GitHub
- An GitHub account

## Setting Up

### Creating an EC2 Instance

1. Launch an EC2 instance using the AWS Management Console.

![Screenshot: Instance](./ScreenShot/creating_instance.png)
   
2. Add a key pair for secure SSH access during instance creation.

![Screenshot:Key Pair](./ScreenShot/keypair.png) 
  
3. Connect to the instance using SSH

![Screenshot:Key Pair](./ScreenShot/connectToInstance.png) 
  

### Installing Jenkins

1. Update packages and install Java:
     ```bash
     sudo apt-get update
     sudo apt-get install openjdk-11-jdk

![Screenshot:Key Pair](./ScreenShot/install_java.png) 


   - Because Jenkins is made up of Java, we need to install Java on our Ubuntu machine.
  
2. Set up the location for Jenkins installation:

     ```bash
     curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
     /usr/share/keyrings/jenkins-keyring.asc > /dev/null
     echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
     https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
     /etc/apt/sources.list.d/jenkins.list > /dev/null
s

3. Install Jenkins:

     ```bash
     sudo apt-get install jenkins
     sudo apt-get update

4. Start Jenkins

     ```bash
     sudo systemctl start jenkins.service
     sudo systemctl status jenkins
   
![Screenshot: Installed Jenkins](./ScreenShot/startjenkins.png)

### Jenkins Setup

1. Open the Jenkins port in your security group:

   - Go to your EC2 instance details in the AWS Management Console.
   - Under the "Security groups" section, click on the security group associated with your instance.
   - In the "Inbound rules" tab, add a custom TCP rule for port 8080.
   - 
![Screenshot: Inbound Rule](./ScreenShot/Security_port.png)

2. Access Jenkins in your browser:

     ```bash
     http://your-instance-ip:8080
   
![Screenshot: Access Jenkins](./ScreenShot/jenkinsScreen.png)

3. Retrieve the initial admin password:

     ```bash
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword

4. Install the suggested plugins and create an admin user.

![Screenshot: Plugins](./ScreenShot/InstallPlugins.png)

5. Create a admin user for jenkins

![Screenshot: UserJenkins](./ScreenShot/CreateanAdminUser.png)
 
6. Start using Jenkins and configure any additional settings as needed.

![Screenshot: Welcome Screen](./ScreenShot/WelcomeJenkinsScreen.png)

### Generating SSH Keys

1. Generate SSH keys on your EC2 instance:

     ```bash
     ssh-keygen
     cd .ssh
     ls
     cat id_rsa
     cat id_rsa.pub

- After this, you will get a Public and Private Key.


### Integrating GitHub and Jenkins

1. Clone the [MERN Stack Project Code](https://github.com/ifeelpankaj/locker) repository from GitHub.

 ![Screenshot: Repo](./ScreenShot/GitRepo.png)
 
2. Go to your GitHub settings:

   - Click on your profile picture in the top right corner and select "Settings".
   - Navigate to "SSH and GPG keys" in the left sidebar.


3. Add a new SSH key:

   - Click on "New SSH key".
   - In your terminal, open the public key file (usually `~/.ssh/id_rsa.pub`) and copy its content (starts with `ssh-rsa`).
   - Paste the public key into the "Key" field.
   - Give your key a meaningful title and click "Add SSH key".
   - 
 ![Screenshot: Plugins](./ScreenShot/Ssh-Github.png)

4. Open your Jenkins dashboard:

   - Create a new "Freestyle project" by clicking "New Item" on the Jenkins homepage.
     
 ![Screenshot: Jenkins Project](./ScreenShot/Createafreestyleproject.png)

5. Configure the project:

   - Add a project name and description.

![Screenshot: Jenkins Description](./ScreenShot/description.png)

   - Under the "Source Code Management" section, select "Git" and enter your GitHub repository URL.

![Screenshot: Jenkins Git Url](./ScreenShot/Git.png)

   - In the "Credentials" dropdown, click "Add" to add your private key. Paste the private key content generated earlier (beginning with `-----BEGIN OPENSSH PRIVATE KEY-----`).

![Screenshot: Jenkins Description](./ScreenShot/JenkinCred1.png)

![Screenshot: Jenkins Description](./ScreenShot/JenkinCred2.png)

![Screenshot: Jenkins Description](./ScreenShot/JenkinCred3.png)

   - Save your configuration.

6. Build the project:

   - Click "Build Now" on the project page.
![Screenshot: Jenkins Description](./ScreenShot/BuildNow.png)
   - Monitor the build's console output to check the location of your project on the server.
![Screenshot: Jenkins Description](./ScreenShot/ConsoleLogJenkins.png)

### Automating Docker Build and Run

#### Install Docker on your EC2 instance

1. Install Docker:

     ```bash
     sudo apt-get install docker.io
     sudo apt-get update

#### Create a Docker File    
1. Create a Dockerfile in your project directory. In my project, it's already present.


![Screenshot: Jenkins Description](./ScreenShot/DockerFile.png)

2. Build Docker Image:

   ```bash
   sudo usermod -a -G docker $USER
   sudo reboot
   cd /var/lib/jenkins/workspace/Jenkins-Master
   docker build . -t doclocker

![Screenshot: Docker](./ScreenShot/DockerContainer.png)

3. Run Docker Container:

      ```bash
      docker run -d --name doclocker -p 8000:8000 doclocker
      docker ps
      
![Screenshot: Docker](./ScreenShot/RunDocker.png)

4. Bind Docker Port to 8000 and Update Security Group:

   -Open your AWS Management Console.
   -Navigate to the EC2 dashboard and select your instance.
   -In the "Security groups" section, click on the associated security group.
   -Add an inbound rule to allow traffic on port 8000.
   -Save the changes.

### Automate Docker Build and Run with Jenkins

1. Go to the Jenkins dashboard.
2. Open your job and navigate to the build steps 
  
      ````bash
      docker build . -t doclocker
      docker run -d --name doclocker -p 8000:8000 doclocker
      
![Screenshot:Jenkins/ Docker](./ScreenShot/JenkinsBuildStep.png)

    -This script includes the Docker commands to build a Docker image named doclocker from the code in your repository and run a Docker container with the image. The -p flag maps port 8000 on your EC2 instance to port 8000 in the container.

3. Save configuration and click on build now 
    -After defining the build steps, save your configuration. Now, click on "Build Now" in the Jenkins job page. Jenkins will automatically retrieve the code from your GitHub repository, create a Docker image, and run the container in the background.

![Screenshot:Jenkins/ Docker](./ScreenShot/3.png)

![Screenshot:Jenkins/ Docker](./ScreenShot/2.png)

![Screenshot:Jenkins/ Docker](./ScreenShot/1.png)


## Conclusion

In this comprehensive guide, we have walked through the process of setting up a robust CI/CD pipeline for your Node.js application using Jenkins, GitHub, and Docker. By following these steps, you've achieved an automated workflow that enhances development efficiency and ensures consistent deployments.

Throughout this guide, you have:

- Created an EC2 instance on AWS to serve as the platform for your CI/CD pipeline.
- Installed Jenkins and configured it to automate various stages of your deployment process.
- Integrated GitHub with Jenkins, allowing seamless code retrieval and building.
- Generated SSH keys for secure communication between Jenkins and your GitHub repository.
- Automated the Docker build and run process, ensuring your application is containerized and deployed efficiently.

By harnessing the power of these tools, you've successfully orchestrated an end-to-end pipeline that handles everything from code changes to running your application in a Docker container. This setup not only streamlines your development workflow but also ensures that your application is deployed consistently across environments.

As you continue to refine and enhance your Node.js application, this CI/CD pipeline will serve as a foundation for maintaining a seamless and reliable development process. Feel free to explore further optimizations, customizations, and integrations to tailor the pipeline to your specific needs.

Congratulations on setting up your Node.js CI/CD pipeline using Jenkins, GitHub, and Docker. Happy coding and deploying!

_Pankaj_