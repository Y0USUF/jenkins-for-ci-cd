pipeline {
  agent any
  tools {
    nodejs "Node18"
  }

  environment {
    IMAGE = "yousufuddin/jenkins-for-ci-cd"
    DOCKERHUB_CRED = "Dockerhub-cred"  
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install') {
      steps {
        bat 'npm install'
      }
    }

    stage('Test') {
      steps {
        bat 'echo No tests to run'
      }
    }

    stage('Build Docker Image') {
      steps {
        bat "docker build -t ${env.IMAGE}:${env.BUILD_NUMBER} ."
      }
    }

    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: "${DOCKERHUB_CRED}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          bat "docker login -u %DOCKER_USER% -p %DOCKER_PASS%"
          bat "docker push ${env.IMAGE}:${env.BUILD_NUMBER}"
          bat "docker tag ${env.IMAGE}:${env.BUILD_NUMBER} ${env.IMAGE}:latest"
          bat "docker push ${env.IMAGE}:latest"
        }
      }
    }
  }

  post {
    always {
      echo "Pipeline finished. Docker image pushed: ${env.IMAGE}:${env.BUILD_NUMBER}"
      echo "This is in Dev branch in git"
    }
  }
}
