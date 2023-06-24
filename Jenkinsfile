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
        withCredentials([sshUserPrivateKey(credentialsId: '38880b8b-9bf4-4dc5-bf28-4d7d74665a4b', keyFileVariable: 'SSH_KEY')]) {
          script {
            // Define your remote machine details
            def remoteMachine = [
              name: 'RemoteMachine', // Add a name for the remote machine
              host: '3.7.71.17',
              user: 'ubuntu',
              allowAnyHosts:true,
              key: SSH_KEY
            ]

            // Start the SSH agent and add the private key
            sshagent(['your-ssh-credential-id']) {
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

    // Rest of the pipeline stages...
  }
}
