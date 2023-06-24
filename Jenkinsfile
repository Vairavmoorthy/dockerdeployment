pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/Vairavmoorthy/dockerdeployment.git'
      }
    }

    stage('Deploy to Remote Machine') {
      steps {
        script {
          // Define your remote machine details
          def remoteMachine = [
            name: 'RemoteMachine',
            host: '3.7.71.17',
            user: 'ubuntu',
            credentialsId: 'u112'
          ]
        }
      }
    }

    stage('Login to Docker') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'Dt20',
          usernameVariable: 'DOCKER_USERNAME',
          passwordVariable: 'DOCKER_PASSWORD'
        )]) {
          sh '''
            echo ${DOCKER_PASSWORD} | sudo -S docker login -u ${DOCKER_USERNAME} --password-stdin
          '''
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
