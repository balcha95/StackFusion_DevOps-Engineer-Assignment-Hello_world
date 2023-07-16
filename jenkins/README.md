# Jenkins Master and Slave Configuration

This guide explains the steps to configure Jenkins Master and Slave nodes. The Master node will host Jenkins, while the Slave nodes will have specific tools and configurations required for the build and deployment process.

## Jenkins Master

### Prerequisites
- Launch an AWS Linux instance with port 8080 and assign a Name tag.
- Update the instance to ensure it is up to date.

### Installation Steps
Connect to the Jenkins Master instance and follow the steps below:

1. Open a terminal or SSH into the instance.
2. Execute the following commands:

```
sudo -i
yum update -y

# Install Jenkins repository
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade

# Install epel package
amazon-linux-extras install epel

# Install Java 11
sudo yum install java-11-openjdk

# Install Jenkins
sudo yum install jenkins
sudo systemctl daemon-reload

# Start Jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

3. Jenkins will start running on port 8080. Access the Jenkins web interface using the instance's public IP address or DNS name.

### Slave Nodes

#### Prerequisites
- Launch AWS Linux instances for the Slave nodes and assign appropriate Name tags.
- Update the instances to ensure they are up to date.

#### Installation Steps
Connect to each Slave node and follow the steps below:

1. Open a terminal or SSH into the instance.
2. Execute the following commands:

```bash
# Install epel package
amazon-linux-extras install epel

# Install Java 11
amazon-linux-extras install java-openjdk11 -y

# Install Git
yum install git -y

# Install Maven
sudo wget https://dlcdn.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.tar.gz
sudo tar xf apache-maven-3.8.8-bin.tar.gz -C /opt

# Create a symlink for Apache Maven directory
sudo ln -s /opt/apache-maven-3.8.8 /opt/maven
```

3. Set the Java path and environment variables:

```
# Check the installed Java version
cd /usr/lib/jvm/
# Note down the Java version path, e.g., /usr/lib/jvm/java-11-openjdk-11.0.19.0.7-1.amzn2.0.1.x86_64

# Open .bash_profile and add the following lines:
export JAVA_HOME="/usr/lib/jvm/java-11-openjdk-11.0.19.0.7-1.amzn2.0.1.x86_64"
export MAVEN_HOME=/opt/apache-maven-3.8.8
export M2=/opt/apache-maven-3.8.8/bin
PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$MAVEN_HOME:$M2

source ~/.bash_profile
source ~/.bashrc
```

4. Repeat the steps for each Slave node.

### Jenkins Node Configuration

1. Login to Jenkins through the browser and navigate to "Manage Jenkins" > "Manage Nodes" > "New Node".
2. Configure the Node Name, Label, and access through SSH.
3. Provide the SSH Username and select "Enter directly" for the Private Key option.
4. Copy the private key from `id_rsa` and paste it into the private key field in Jenkins.
5. Save the configuration.

### Global Tools Configuration
1. Go to "Manage Jenkins" > "Global Tool Configuration".
2. Under the "Maven" section, add the Maven installation details and save the configuration.

## Docker Installation

1. Install Docker using the following command:

```
yum install docker -y
```

2. Start and enable the Docker service:

```
systemctl start docker
systemctl enable docker
systemctl status docker
```

3. Add the `devopsadmin` user to the Docker group:

```
usermod -aG docker devopsadmin
```

4. Docker is now installed and ready to use.

