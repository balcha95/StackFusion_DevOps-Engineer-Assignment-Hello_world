# StackFusion DevOps Engineer Assignment - Hello World

This project showcases the implementation of various DevOps practices and technologies to deploy a "Hello World" application. The project covers the following tasks using Git, GitHub, Jenkins, Maven build tool, Docker, Kubernetes, Prometheus, and Grafana:

## Task 1: Infrastructure as Code (IaC)

Phase I: Infrastructure Provisioning
- Launched 5 EC2 instances using Terraform:
  - Jenkins_Master: Jenkins master server for CI/CD pipeline.
  - Jenkins_Slave: Jenkins slave server for building applications.
  - KuberMaster: Kubernetes master server for managing the cluster.
  - Kubernetes WN1: Kubernetes worker node for running application workloads.
  - Monitoring server: Server for hosting Prometheus, Grafana, and Node Exporters.

Phase II: Tools Installation and Configuration
- Installed and configured the required tools on each server:
  - Jenkins_Master: git, JDK, Jenkins.
  - Jenkins_Slave: git, JDK, Maven, Docker.
  - KuberMaster: Kubernetes configuration files for installation.
  - Kubernetes WN1: Kubernetes configuration files for installation.
  - Monitoring server: Prometheus, Grafana, and Node Exporters.

## Task 2: Continuous Integration/Continuous Deployment (CI/CD)

Implemented an end-to-end CI/CD pipeline:
- Stage 1: SCM Checkout & Maven Build
- Stage 2: Docker build, Login to DockerHub, Push to DockerHub
- Stage 3: Deployment to Kubernetes Cluster
- Stage 4: Monitor the servers using Monitoring Tools

## Task 3: Monitoring and Logging

Implemented basic monitoring and logging using Prometheus and Grafana:
- Monitored the web server created in Task 1 and collected relevant metrics such as CPU usage, memory usage, and response time.
- Visualized the collected metrics in a dashboard using Grafana.
- Set up logging to capture application logs and store them centrally for easy access and analysis.

## Task 4: Kubernetes and Microservices Architecture

Created a microservice-centric application and set up Kubernetes services for local development.
