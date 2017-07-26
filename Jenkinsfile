#!groovy

node(){
	withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'GleSYSProjectCl26817', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {

		sh 'echo uname=$USERNAME pwd=$PASSWORD'

	 }


	stage('Checkout source'){
		checkout scm
		sh 'echo uname=$USERNAME pwd=$PASSWORD'

	}
	stage('Build docker image'){
		//test
	}

 }
