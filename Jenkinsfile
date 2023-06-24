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
            identityFile: [
              credentialsId: '38880b8b-9bf4-4dc5-bf28-4d7d74665a4b',
              variable: 'SSH_KEY'
            ],
            allowAnyHosts: true
          ]

          // Start the SSH agent and add the private key
          sshagent(['38880b8b-9bf4-4dc5-bf28-4d7d74665a4b']) {
            // Establish SSH connection to the remote machine
            sshCommand remote: remoteMachine, command: '''
              sudo docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD $DOCKER_REGISTRY
              sudo docker pull vairav7590/vairav
              sudo docker run -d -p 9090:80 vairav7590/vairav
            '''
          }
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
          sh 'sudo docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD $DOCKER_REGISTRY'
        }
      }
    }

    stage('Pull Image') {
      steps {
        sh 'sudo docker pull vairav7590/vairav'
