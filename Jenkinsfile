pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/Vairavmoorthy/dockerdeployment.git'
      }
    }

    stage('Login to Docker') {
      steps {
        withCredentials([usernamePassword(
            credentialsId: 'Dt20',
            usernameVariable: 'DOCKER_USERNAME',
            passwordVariable: 'DOCKER_PASSWORD'
          )]) {
          sh 'sudo docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD $DOCKER_REGISTRY'
        }
      }
    }

    stage('Pull Image') {
      steps {
        sh 'sudo docker pull vairav7590/vairav'
      }
    }

    stage('Deploy') {
      steps {
        sh 'sudo docker run -d -p 9090:80 vairav7590/vairav'
      }
    }
  }
}

