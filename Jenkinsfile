pipeline {
  agent {
    node {
      label "linux && java17"
    }
  }
  
  stages {
    stage('Build') {
        steps {
          echo 'Building Stage 1'
          echo 'Building Stage 2'
          echo 'Building Stage 3'
        }
    }
    stage('Test') {
        steps {
          echo 'Testing Stage 1'
          echo 'Testing Stage 2'
          echo 'Testing Stage 3'
        }
    }
    stage('Deploy') {
        steps {
          echo 'Deploying Stage 1'
          echo 'Deploying Stage 2'
          echo 'Deploying Stage 3'
        }
    }
  }
  
  post {
    always {
      echo "I will always say hello"
    }
    success {
      echo "Pipeline succed"
    }
    failure {
      echo "Pipeline failed"
    }
    cleanup {
      echo "Dont care success or fail"
    }
  }
}