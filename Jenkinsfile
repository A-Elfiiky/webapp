pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker-compose build -t aelfiiky/jenkins-docker-hub:v1 .'
        echo 'Docker-compose-build Build Image Completed' 
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push aelfiiky/jenkins-docker-hub:v1'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
