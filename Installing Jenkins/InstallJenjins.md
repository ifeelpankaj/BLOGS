# Installing Jenkins on AWS

This guide will walk you through the process of setting up Jenkins on an Amazon Web Services (AWS) instance. Jenkins is a widely used automation server that can be used for continuous integration, continuous delivery, and more.

## Prerequisites

- An AWS account. If you don’t have one, you can register [here](https://aws.amazon.com/aispl/registration-confirmation/).
- Basic knowledge of terminal commands.


## Step 1: Launch an EC2 Instance

1. Before you proceed with installing Jenkins, you'll need to launch an EC2 instance on AWS. Follow the steps below:

2. Please refer to the detailed documentation : [To Launch Your EC2 Instance](link_to_your_documentation)



## Step 2: Update & Install Java 

Update the package list & Install OpenJDK 11:
    
    ```bash
    sudo apt-get update
    sudo apt install openjdk-11-jdk

## Step 3: Add Jenkins Repository

Add the Jenkins repository key::
    
    ```bash
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee   /usr/share/keyrings/jenkins-keyring.asc > /dev/null



Add the Jenkins repository to your system:
    
    ```bash
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]   https://pkg.jenkins.io/debian-stable binary/ | sudo tee   /etc/apt/sources.list.d/jenkins.list > /dev/null
    

## Step 4: Install Jenkins


Update the package list again:
    
    ```bash
    sudo apt-get update

Install Jenkins:
    
    ```bash
    sudo apt install jenkins


## Step 5: Start Jenkins

Start the Jenkins service:
    
    ```bash
    sudo systemctl start jenkins


Enable Jenkins to start on boot:
    
    ```bash
    sudo systemctl enable jenkins


## Step 6: Access Jenkins

Open your web browser and navigate to: http://your-machine-ip:8080

    - Make Sure 8080 Port is Added in security group

Retrieve the Jenkins initial admin password:

## Step 7: Congratulations!

You've successfully installed jenkins on your AWS machine.
    

