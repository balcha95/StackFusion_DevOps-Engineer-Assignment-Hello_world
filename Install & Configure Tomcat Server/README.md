# Install & Configure Tomcat Server

This section provides step-by-step instructions on how to install and configure the Tomcat server on an AWS EC2 Linux instance.

## Prerequisites

Before proceeding with the installation and configuration of the Tomcat server, ensure you have the following prerequisites in place:

- Launch an AWS EC2 Linux instance.
- Connect to the EC2 instance using SSH.

## Installation Steps

1. Connect to the EC2 instance using SSH by running the following command:

   ```bash
   ssh ec2-user@<ec2-instance-public-ip>
   ```

   Replace `<ec2-instance-public-ip>` with the public IP address of your EC2 instance.

2. Update the system packages by running the following command:

   ```bash
   sudo yum update -y
   ```

3. Install the Epel package by running the following command:

   ```bash
   sudo amazon-linux-extras install epel
   ```

4. Install Java Development Kit (JDK) by running the following command:

   ```bash
   sudo yum install java-1.8.0-openjdk-devel -y
   ```

5. Set the Java path and environment variables by editing the `.bashrc` file:

   ```bash
   nano ~/.bashrc
   ```

   Add the following lines at the end of the file:

   ```bash
   export JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk"
   PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
   ```

   Save the file and exit the editor.

6. Update the `.bash_profile` file by running the following command:

   ```bash
   nano ~/.bash_profile
   ```

   Add the following line at the end of the file:

   ```bash
   export JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk"
   ```

   Save the file and exit the editor.

7. Load the updated `.bash_profile` file by running the following command:

   ```bash
   source ~/.bash_profile
   ```

8. Download and install Tomcat by running the following commands:

   ```bash
   cd /opt
   sudo wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.90/bin/apache-tomcat-8.5.90.tar.gz
   sudo tar -xvzf apache-tomcat-8.5.90.tar.gz
   sudo mv apache-tomcat-8.5.90 tomcat
   ```

9. Start the Tomcat server by running the following command:

   ```bash
   cd /opt/tomcat/bin
   sudo ./startup.sh
   ```

   The Tomcat server should now be running on port 8080.

## Add User for Tomcat

To add a user for Tomcat, follow these steps:

1. Create a new user by running the following command:

   ```bash
   sudo useradd -m -d /home/devopsadmin devopsadmin
   ```

2. Switch to the newly created user by running the following command:

   ```bash
   sudo su - devopsadmin
   ```

3. Generate an SSH key pair for the user by running the following command:

   ```bash
   ssh-keygen
   ```

4. Copy the public key to the authorized keys file by running the following command:

   ```bash
   cat ~/.ssh/id_rsa.pub > ~/.ssh/authorized_keys
   ```

5. Set the correct permissions for the `.ssh` directory and the `authorized_keys` file by running the following commands:

   ```bash
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
   ```

6. Change the ownership of the Tomcat directory to the newly created user by running the following command:

   ```bash
   sudo chown -R devopsadmin /opt/tomcat
   ```

Now you have successfully installed and configured the Tomcat server on your AWS EC2 Linux instance.

## Configure Jenkins

To configure Jenkins to deploy the Tomcat server, follow these steps:

1. Access the Jenkins master through a web browser.

2. Install the "Publish Over SSH" plugin in Jenkins.

3. Go to "Manage Jenkins" -> "Configure System" -> "Configure Publish Over SSH Plugin".

4. Configure the necessary SSH credentials for connecting to the Tomcat server.

5. Create a Jenkins freestyle job to test the deployment by specifying the location of the Tomcat WAR file.

   Example:
   - WAR File Path: `/opt/tomcat/webapps/target/mvn-hello-world.war`

Make sure to adapt the paths and filenames according to your specific setup.

