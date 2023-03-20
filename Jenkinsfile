pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages {
        stage('Build and Push Docker images') {
            steps {
                sh 'docker build -t aelfiiky/flaskapp ./flaskapp'
                sh 'docker build -t aelfiiky/db ./db'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push aelfiiky/flaskapp'
                sh 'docker push aelfiiky/db'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
