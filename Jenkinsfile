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
              credentialsId: 'u112',
              variable: 'SSH_KEY'
            ],
            allowAnyHosts: true
          ]

          // Start the SSH agent and add the private key
          sshagent(['u112']) {
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
  }
}
