# StackFusion DevOps Engineer Assignment - Hello World

This project showcases the implementation of various DevOps practices and technologies to deploy a "Hello World" application. The project covers the following tasks using Git, GitHub, Jenkins, Maven build tool, Docker, Kubernetes, Prometheus, and Grafana.

This project demonstrates the implementation of Infrastructure as Code (IaC) using Terraform ansible and the setup of a basic CI/CD pipeline using Git, Jenkins, Maven, Docker, and Kubernetes. It also includes the implementation of monitoring and logging using Prometheus, Grafana.

## Prerequisites
Before you begin, make sure you have the following prerequisites installed on your system:
- Visual Studio Code
- Terraform CLI
- Git
- Jenkins
- Maven
- Docker
- Kubernetes
- Prometheus
- Grafana

## Task 1: Infrastructure as Code (IaC)
The `terraform` directory contains the necessary scripts and configuration files to provision a web server infrastructure. Follow the instructions provided in the `terraform/README.md` file to provision the infrastructure, install and configure a Linux-based operating system, web server software (Apache Tommcat), SSL/TLS encryption, and firewall rules.

## Task 2: Continuous Integration/Continuous Deployment (CI/CD)
The `jenkins` directory contains the necessary files and configurations to set up a basic CI/CD pipeline. Follow the instructions provided in the `jenkins/README.md` file to configure Jenkins, create a Jenkins job to automate the build process, and deploy the application to the web server provisioned in Task 1.

## Task 3: Monitoring and Logging
The `monitoring` directory contains the necessary files and configurations to set up monitoring and logging using Prometheus, Grafana. Follow the instructions provided in the `monitoring/README.md` file to configure Prometheus to monitor the web server metrics and Grafana to visualize the metrics.

## Task 4: Kubernetes and Microservices Architecture
The `kubernetes` directory contains the necessary files and configurations to deploy a microservice-centric application using Kubernetes. Follow the instructions provided in the `kubernetes/README.md` file to deploy the application as a mediator between a client and your local system. The mediator will communicate with the client application and send the appropriate response.
