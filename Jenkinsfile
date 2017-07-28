pipeline {
    agent any
    environment {
        MACHINE_DRIVER = credentials('glesys_docker_driver')
	MACHINE_STORAGE_PATH = credentials('MACHINE_STORAGE_PATH') 
	DOCKER_HOST = "tcp://109.74.13.214:2376"
        DOCKER_CERT_PATH = "/home/jenkins/machines/manager1"
        DOCKER_TLS_VERIFY = "1"
        LOADBALANCER = credentials('myapp_loadbalancer')
	PROJECT = credentials('GleSYSProjectCl26817')
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
        stage('Prepare loadbalancer and reduce traffic levels to BLUE services') {
           steps {
                sh '''TARGETS=$(curl -s -X POST --data-urlencode "loadbalancerid=$LOADBALANCER" -k --basic -u $PROJECT_USR:$PROJECT_PSW https://api.glesys.com/loadbalancer/details/format/json | jq -r '.response.loadbalancer.backends[].targets[] | select(.port==81) | [.name] | @tsv') \

		   for TARGET1 in $TARGETS; do \
                   curl -s -X POST --data-urlencode "loadbalancerid=$LOADBALANCER" --data-urlencode "backendname=be5979dd85c2c41" --data-urlencode "targetname=$TARGET1" --data-urlencode "weight=10" -k --basic -u $PROJECT_USR:$PROJECT_PSW https://api.glesys.com/loadbalancer/edittarget/; done'''
            }
        }
	stage('Deploy BLUE services to Swarm') {
           environment {
               STACK = "BLUE" 
           }
           steps {
                sh 'docker stack deploy --compose-file docker-compose-swarm.yml MyAppBlue'
            }
        }
        stage('Approve build and deploy to GREEN') {
            steps {	    
                input "Approve Blue build?"
            }
        }
	stage('Restore traffic levels to BLUE services') {
           steps {
                sh '''TARGETS=$(curl -s -X POST --data-urlencode "loadbalancerid=$LOADBALANCER" -k --basic -u $PROJECT_USR:$PROJECT_PSW https://api.glesys.com/loadbalancer/details/format/json | jq -r '.r$

                   for TARGET1 in $TARGETS; do \
                   curl -s -X POST --data-urlencode "loadbalancerid=$LOADBALANCER" --data-urlencode "backendname=be5979dd85c2c41" --data-urlencode "targetname=$TARGET1" --data-urlencode "weight=1" -k --$
            }
        }
	stage('Deploy GREEN services to Swarm') {
           environment {
               STACK = "GREEN"
           }
           steps {
                sh 'docker stack deploy --compose-file docker-compose-swarm-green.yml MyAppGreen'
            }
        }	
    }
}
