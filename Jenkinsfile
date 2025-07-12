pipeline {
  agent none

  stages {
    stage('Build') {
      agent {
        node {
          label "linux && java17"
        }
      }
      steps {
        script {
          for (int i = 0; i <10; i++) {
            echo ("Script ${i}")
          }
        }
        echo 'Building Stage Start'
        sh('./mvnw clean compile test-compile')
        echo 'Building Stage Complete'
      }
    }

    stage('Test') {
      agent {
        node {
          label "linux && java17"
        }
      }
      steps {
        script {
          def data = [
            "firstname": "Vincent",
            "lastname": "Khoe"
          ]
          writeJSON(file: "data.json", json: data)
        }
        echo 'Testing Stage Start'
        sh('./mvnw test')
        echo 'Testing Stage Complete'
      }
    }

    stage('Deploy') {
      agent {
        node {
          label "linux && java17"
        }
      }
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