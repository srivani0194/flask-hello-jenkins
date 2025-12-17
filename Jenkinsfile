pipeline {
  agent any

  environment {
    IMAGE = "flask-hello:${BUILD_NUMBER}"
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Test (Python container)') {
      agent {
        docker {
          image 'python:3.12-slim'
          args '-u root:root'   // avoids permission issues writing in workspace
        }
      }
      steps {
        sh '''
          python --version
          pip install --no-cache-dir -r requirements.txt -r requirements-dev.txt
          pytest -q
        '''
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE .'
      }
    }

    stage('Security Scan (Trivy)') {
      steps {
        sh '''
          docker run --rm \
            -v /var/run/docker.sock:/var/run/docker.sock \
            aquasec/trivy:latest image \
              --severity HIGH,CRITICAL \
              --exit-code 1 \
              --no-progress \
              $IMAGE
        '''
      }
    }
  }
}
