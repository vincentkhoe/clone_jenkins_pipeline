pipeline {
  agent {
    node {
      label "linux && java17"
    }
  }
  
  stages {
    stage('Build') {
        steps {
          echo 'Building Stage Start'
          sh('./mvnw clean compile test-compile')
          echo 'Building Stage Complete'
        }
    }
    stage('Test') {
        steps {
          echo 'Testing Stage Start'
          sh('./mvnw test')
          echo 'Testing Stage Complete'
        }
    }
    stage('Deploy') {
        steps {
          echo 'Deploying Stage 1'
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