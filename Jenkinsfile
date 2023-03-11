pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
      stage('checkout from scm'){
          steps{
               git branch: 'main', url: 'https://github.com/gangarampadolkar93/jenkins_image.git'
          }
      }
    stage('Compile code') {
      steps {
        sh 'docker build -t gangarampadolkar/gangaram_jenkins_image .'
      }
    }
    stage('Login to Docker ') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push to Docker hub') {
      steps {
        sh 'docker push gangarampadolkar/gangaram_jenkins_image'
      }
    }
  }
 }
