pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
               checkout scmGit(branches: [[name: '*/dev']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Karthick9911/App-Deploy.git']])
            }
        }
        stage('Build') {
            steps {
               sh 'chmod +x build.sh'
               sh './build.sh'
            }
        }
	      stage('Push Docker Image'){
	          steps {
	             script {
		              withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]){
		                 sh 'docker login -u karthick9911 -p ${dockerhubpwd}'
		                 sh 'docker push karthick9911/dev'
	                }	
	             }
	         }
        }
    }
}
