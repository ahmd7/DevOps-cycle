# DevOps Pipeline for Laravel Application

This comprehensive guide outlines the deployment pipeline for a Laravel application, leveraging Docker containers orchestrated via Docker Compose, with automation facilitated by Ansible, Terraform, and Jenkins. Below are detailed instructions for each step of the setup and deployment process.

## Components:

### 1. Dockerfile:

The Dockerfile is used to construct the PHP-Apache image required for hosting the Laravel application.

### 2. docker-compose:

docker-compose is employed to compartmentalize the application into microservices, including PHP-Apache, MySQL, and PHPMyAdmin.

### 3. ansible-playbooks:

Ansible playbooks automate the build process of the Dockerfile and docker-compose.yml for seamless deployment.

### 4. Terraform:

Terraform scripts automate the provisioning of infrastructure, specifically for setting up the Jenkins EC2 instance.

### 5. Jenkins:

Jenkins serves as the automation hub for deploying the Laravel application.
## App structure
![DevOps cycle](https://drive.google.com/file/d/1dNuTfyW8Kt5rKQ6yYSvUx8uTAHqOrB39/view?usp=sharing)

## Setup Instructions:

### Step 1: Build Jenkins EC2 Instance

```bash
$ cd terraform
$ terraform init
$ terraform plan
$ terraform apply -auto-approve
```
### Step 2: Connect to the EC2 by SSH
```bash
$ ssh -i file.pem ec2-user@<Public IPv4 DNS>
```
### Step 3: Create sh file
```bash
$ vim install.sh
$ chmod +x install.sh
$ ./install.sh
```
### Step 4: Verify Installation
```bash
java -version
jenkins --version
docker --version
ansible --version
docker-compose --version
eksctl version
minikube version
k9s version
aws --version
```
### Step 5: Access Jenkins UI
Visit `<ec2-Public IPv4 DNS>:8080` in your web browser to access the Jenkins UI and complete the setup.

### Step 6: Create 1st Jenkins job
Create a Jenkins job for running docker-compose on the EC2 instance. Add the GitHub repository URL and credentials, then execute the following command in the Jenkins job's shell:

```bash
Create a Jenkins job for running docker-compose on the EC2 instance. Add the GitHub repository URL and credentials, then execute the following command in the Jenkins job's shell:
```
### step 7: Configure GitHub Webhook for Jenkins
1- In your GitHub repository, go to "Settings" -> "Webhooks" -> "Add webhook."
2- Set the Payload URL to `<JENKINS_URL>/github-webhook/.`
3- Set the Content type to "application/json."
4- Set the webhook events to "Just the push event."
5- Ensure the webhook is active and save.

### Step 8: Update Composer in PHP-Apache Container
Ensure Composer is updated inside the running PHP-Apache container. Use the following command:
```bash
docker exec -it <PHP_APACHE_CONTAINER_NAME> composer update
```
### Step 9: Access the Application
Access the Laravel application at:

- `<ec2-Public IPv4 DNS>:5000`
- `<ec2-Public IPv4 DNS>:4000`




