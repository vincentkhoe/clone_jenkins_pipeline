pipeline {
  agent {
    node {
      label "linux && java17"
    }
  }
  
  stages {
      stage('Hello') {
          steps {
              echo 'Hello World'
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