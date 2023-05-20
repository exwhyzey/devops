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
        sh 'docker build -t  exwhyzeygmail/jenkins-docker-hub:nginx-devops-v$BUILD_NUMBER .'
      }
    }
    stage('Login') {
  steps {
  sh 'echo $DOCKERHUB_CREDENTIALS | docker login -u $DOCKERHUB_CREDENTIALS --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push exwhyzeygmail/jenkins-docker-hub:nginx-devops-v$BUILD_NUMBER'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
