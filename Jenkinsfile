pipeline {
  agent {
    node {
      label "linux && java17"
    }
  }
  
  stages {
    stage('Build') {
        steps {
            echo 'Building Stage'
        }
    }
    stage('Test') {
        steps {
            echo 'Testing Stage'
        }
    }
    stage('Deploy') {
        steps {
            echo 'Deploying Stage'
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