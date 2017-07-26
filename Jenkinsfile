pipeline {
    agent any
    environment {
        MACHINE_DRIVER = credentials('glesys_docker_driver')
	MACHINE_STORAGE_PATH = credentials('MACHINE_STORAGE_PATH') 
    }
    stages {
        stage('Show workspace') {
            steps {
                sh 'ls -la'
            }
	}
	stage('Build docker image') {
            steps {
		env.DOCKER_HOST = "tcp://109.74.13.214:2376"
		env.DOCKER_CERT_PATH = "/home/jenkins/machines/manager1"
		env.DOCKER_TLS_VERIFY = "1"
                sh 'docker node ls'
            }
	
        }
    }
}
