#!groovy

pipeline{
    agent any
    environment{
		 MACHINE_DRIVER = credentials('glesys_docker_driver')
        }
    stages{
        stage('Checkout source') {
	    steps {
			checkout scm
		 }	
	}
       stage('Build docker image') {		
           steps {
			//Build
		 }
	}

 }
}
