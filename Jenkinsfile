pipeline {
    agent { label 'slavenode1' }
	

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

	environment {	
		DOCKERHUB_CREDENTIALS=credentials('new_docker_id')
	} 
    
     stages {
        stage('SCM Checkout') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/balcha95/Java-mvn-app2.git'
            }
		}
        stage('Maven Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
			post {
                   //If Maven was able to run the tests.even if some of the test
                  //failed, record the test results and archive the jar file.
              success{
                    sh "cp target/mvn-hello-world.war /home/devopsadmin"
                     }
                 }
        }         
        stage("Docker build"){
	        steps {
			    sh 'docker version'
				sh "docker build -t balcha/mvn-eta-app:${BUILD_NUMBER} ."
				sh 'docker image list'
				sh "docker tag balcha/mvn-eta-app:${BUILD_NUMBER} balcha/mvn-eta-app:latest"
	            }
	    }
	    stage('Login2DockerHub') {
            steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			} 
        }      
        stage('Push2DockerHub') {

			steps {
				sh "docker push balcha/mvn-eta-app:latest"
			}
		}
    }
}
