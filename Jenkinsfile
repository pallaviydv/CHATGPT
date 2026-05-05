pipeline {
  agent any

  environment {
    IMAGE = "plvydv/app"
  }

  stages {

    stage('Clone') {
      steps {
        git 'https://github.com/pallaviydv/CHATGPT.git'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t $IMAGE:latest .'
      }
    }

    stage('Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker-cred', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh 'echo $PASS | docker login -u $USER --password-stdin'
          sh 'docker push $IMAGE:latest'
        }
      }
    }
  }
}