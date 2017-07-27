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
                sh 'docker-compose build'
            }
        }
	stage('Publish images to registry') {
            steps {
                sh 'docker images'
		sh 'docker tag deploymyapp_nginx:latest registry.dontping.me:5000/deploymyapp_nginx'
		sh 'docker tag deploymyapp_fpm:latest registry.dontping.me:5000/deploymyapp_fpm'
		sh 'docker push registry.dontping.me:5000/deploymyapp_nginx'
		sh 'docker push registry.dontping.me:5000/deploymyapp_fpm'
            }
        }
	stage('Deploy blue services to Swarm') {
           steps {
                sh 'docker stack deploy --compose-file docker-compose-swarm.yml MyAppBlue
'
            }
        }



    }
}
