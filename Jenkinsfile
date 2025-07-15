pipeline {
  agent any

  environment {
    // Optional: make the Socket API key available globally
    SOCKET_SECURITY_API_KEY = credentials('SOCKET-API')
  }

  stages {
    stage('Run Socket') {
      steps {
        withCredentials([string(credentialsId: 'SOCKET-API', variable: 'SOCKET_SECURITY_API_KEY')]) {
          sh '''
            python3 -m venv .venv
            . .venv/bin/activate
            pip install --upgrade socketsecurity
            socketcli --api_token=$SOCKET_SECURITY_API_KEY --target_path .
          '''
        }
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'socket-report.json', onlyIfSuccessful: false
    }
  }
}