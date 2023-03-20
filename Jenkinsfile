pipeline {
    agent any
    tools {
        git 'Default'    
    stages {
        stage('Build and Push Docker images') {
            steps {
                git 'https://github.com/A-Elfiiky/webapp.git'
                sh 'docker build -t fikky/flaskapp ./flaskapp'
                sh 'docker build -t fikky/db ./db'
                withCredentials([string(credentialsId: 'DOCKER_HUB_CREDENTIALS', variable: 'DOCKER_HUB_CREDENTIALS')]) {
                    sh "docker login -u <aelfiiky/jenkins-docker-hub> -p $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                    sh 'docker push fikky/flaskapp'
                    sh 'docker push fikky/db'
                }
            }
        }
    }
}
