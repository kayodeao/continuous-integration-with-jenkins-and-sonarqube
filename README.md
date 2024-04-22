# Continuous Integration Documentation

## Overview

This document outlines the process of integrating GitHub, Jenkins, and SonarQube to automate code scanning and generate reports for code quality and security vulnerabilities.

## Architecture

![Architecture Diagram](link-to-your-diagram)

### Components

1. **GitHub**: Version control repository hosting our codebase.
2. **Jenkins**: Automation server for continuous integration and deployment.
3. **SonarQube**: Platform for static code analysis to detect code smells, bugs, and security vulnerabilities.

## Setup Instructions

### Pre-requisites

- [ ] Two VM instances in Google Cloud Platform (GCP) with Debian 11 image.
- [ ] Access to GitHub repository containing the codebase.

### Step 1: Install Jenkins

1. SSH into your Jenkins VM instance.
2. Install OpenJDK 17
3. Install Jenkins using the following commands:
   ```bash
   sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
   https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
   echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
   https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
   sudo apt-get update
   sudo apt-get install jenkins

4. Start the Jenkins service:
   ```bash
   sudo systemctl start jenkins
   sudo systemctl enable jenkins

### Step 2: Install SonarQube
1.  SSH into your SonarQube VM instance.
2.  Install SonarQube using Docker:
   ```bash
docker pull sonarqube
```
3.  Run SonarQube
```bash
docker run -d --name sonarqube-db -e POSTGRES_USER=sonar -e POSTGRES_PASSWORD=sonar -e POSTGRES_DB=sonarqube postgres:alpine
```


```bash
docker run -d --name sonarqube -p 9000:9000 --link sonarqube-db:db -e SONAR_JDBC_URL=jdbc:postgresql://db:5432/sonarqube -e SONAR_JDBC_USERNAME=sonar -e SONAR_JDBC_PASSWORD=sonar sonarqube
```
4. Access SonarQube at `http://sonarqube-vm-ip:9000` and set up the admin credentials.

   

