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

    stage('Pull Image') {
      steps {
        sh 'docker pull vairav7590/vairav'
      }
    }

    stage('Deploy') {
      steps {
        sh 'docker run -d -p 9090:80 vairav7590/vairav'
      }
    }
  }
}
