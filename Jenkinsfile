pipeline {
  agent none

  environment {
    AUTHOR = "Vincent Khoe"
    EMAIL = "vincentkhoe@gmail.com"
    WEB = "http://www.vincentkhoe.com"
  }

  options {
    disableConcurrentBuilds()
    timeout(time:10, unit: 'MINUTES')
  }

  stages {
    stage('Prepare') {
      environment {
        APP = credentials("vincent_secret")
      }

      agent {
        node {
          label "linux && java17"
        }
      }

      steps {
        echo ("Author: ${AUTHOR}")
        echo ("Email: ${EMAIL}")
        echo ("Web: ${WEB}")
        echo ("APP User: ${APP_USR}")
        sh ('echo "APP Password: $APP_PSW" > "secret.txt"')
        sh ("echo 'APP Password: ${APP_PSW}' > 'secret2.txt'")
        echo ("Start Job: ${env.JOB_NAME}")
        echo ("Start Build: ${env.BUILD_NUMBER}")
        echo ("Branch Name: ${env.BRANCH_NAME}")
      }
    }

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