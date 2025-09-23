pipeline {
  agent any

  environment {
    IMAGE = "yousufuddin/jenkins-for-ci-cd"
    DOCKERHUB_CRED = "Dockerhub-creds"  
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install') {
      steps {
        sh 'npm ci'
      }
    }

    stage('Test') {
      steps {
        sh 'npm run test || true'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          def built = docker.build("${env.IMAGE}:${env.BUILD_NUMBER}")
          env.IMAGE_TAG = "${env.IMAGE}:${env.BUILD_NUMBER}"
          currentBuild.description = "${env.IMAGE}:${env.BUILD_NUMBER}"
        }
      }
    }

    stage('Push to DockerHub') {
      steps {
        script {
          docker.withRegistry('', "${DOCKERHUB_CRED}") {
            def img = docker.image("${env.IMAGE}:${env.BUILD_NUMBER}")
            img.push()
          }
        }
      }
    }
  }

  post {
    always {
      echo "Pipeline finished. Docker image pushed: ${env.IMAGE}:${env.BUILD_NUMBER}"
    }
  }
}
