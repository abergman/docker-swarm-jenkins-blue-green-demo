pipeline {
    agent any
    environment {
        MACHINE_DRIVER = credentials('glesys_docker_driver')
	MACHINE_STORAGE_PATH = credentials('MACHINE_STORAGE_PATH') 
	DOCKER_HOST = "tcp://109.74.13.214:2376"
        DOCKER_CERT_PATH = "/home/jenkins/machines/manager1"
        DOCKER_TLS_VERIFY = "1"
    }
    stages {
        stage('Show workspace') {
            steps {
                sh 'ls -la'
            }
	}
	stage('Build docker image') {
            steps {
                sh 'docker node ls'
            }
	
        }
    }
}
