pipeline {
  agent any
    environment {
      DOCKER_IMAGE_NAME = "maksimzuev/dd_django"
    }
  stages {  
    stage('Build Docker Image') {
      steps {
          script {
              app = docker.build(DOCKER_IMAGE_NAME, "-f Dockerfile.django .")
          }
      }
    }
    stage('Push Docker Image') {
      steps {
          script {
              docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_login') {
                  app.push("${env.BUILD_NUMBER}")
                  app.push("latest")
              }
          }
      }
    }
    stage('DeployToProduction') {
      steps {
          input 'Deploy to Production?'
          milestone(1)
          //implement Kubernetes deployment here
      }
    }
  }
}
