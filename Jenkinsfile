pipeline {
    agent any
    environment {
        MACHINE_DRIVER = credentials('glesys_docker_driver')
	MACHINE_STORAGE_PATH credentials('MACHINE_STORAGE_PATH') 
    }
    stages {
        stage('Show workspace') {
            steps {
                sh 'ls -la'
            }
	}
	stage('Build docker image') {
            steps {
                sh 'docker-machine ls'
            }
	
        }
    }
}
