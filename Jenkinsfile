pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm: [$class: 'GitSCM', branches: [[name: '*/dev']], userRemoteConfigs: [[url: 'https://github.com/Karthick9911/App-Deploy.git']]]
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'chmod +x build.sh'
                    sh './build.sh'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                    script {
                        sh "docker login -u karthick9911 -p $dockerhubpwd"
                        sh 'docker push karthick9911/prod'
                    }
                }
        }
    }
}
