pipeline {
  agent any

  stages {
    stage('Test') {
      steps {
        sh 'pytest -q'
      }
    }

    stage('Build Image') {
      steps {
        sh 'docker build -t flask-hello:${BUILD_NUMBER} .'
      }
    }

    stage('Security Scan') {
      steps {
        sh '''
        docker run --rm \
          -v /var/run/docker.sock:/var/run/docker.sock \
          aquasec/trivy:latest image \
          --severity HIGH,CRITICAL \
          --exit-code 1 \
          flask-hello:${BUILD_NUMBER}
        '''
      }
    }
  }
}
