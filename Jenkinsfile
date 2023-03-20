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
                sh 'docker build -t Aelfiiky/flaskapp ./flaskapp'
                sh 'docker build -t Aelfiiky/db ./db'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push Aelfiiky/flaskapp'
                sh 'docker push Aelfiiky/db'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
