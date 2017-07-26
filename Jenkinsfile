pipeline {
    agent any
    environment {
        MACHINE_DRIVER = credentials('glesys_docker_driver') 
    }
    stages {
        stage('Show workspace') {
            steps {
                sh 'ls -la'
            }
	}
	stage('Build docker image') {
            steps {
                echo "$MACHINE_DRIVER"
            }
	
        }
    }
}
