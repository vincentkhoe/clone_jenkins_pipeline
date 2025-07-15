pipeline {
  agent none

  environment {
    AUTHOR = "Vincent Khoe"
    EMAIL = "vincentkhoe@gmail.com"
    WEB = "http://www.vincentkhoe.com"
  }

  triggers {
    //cron("*/5 * * * *")
    //pollSCM (*/5 * * * *)
    upstream (upstreamProjects: 'Learn Jenkins', threshold: hudson.model.Result.SUCCESS)
  }

  parameters {
    string(name: 'NAME', defaultValue: 'Guest', description: 'What is your name?')
    text(name: 'DESCRIPTION', defaultValue: '', description: 'Tell me about you')
    booleanParam(name: 'DEPLOY', defaultValue: false, description: 'Need to deploy or not?')
    choice(name: 'SOCIAL_MEDIA', choices: ['Instagram','Twitter','X','Tik Tok'], description: 'Which social media?')
    password(name: 'SECRET', defaultValue: '', description: 'Encrypt Key')
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

      failFast true

      parallel {
        stages {
          stage ('Prepare Java') {
            agent {
              node {
                label "linux && java17"
              }
            }

            steps {
              echo "Preparing Java"
              sleep (5)
            }
          }

          stage ('Prepare ENV Variable'){
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
              sleep (5)
            }
          }
        }
      }
    }

    stage('parameters') {
      agent {
        node {
          label "linux && java17"
        }
      }

      steps {
        echo ("Hello: ${params.NAME}")
        echo ("Description: ${params.DESCRIPTION}")
        echo ("Deploy Status: ${params.DEPLOY}")
        echo ("Social Media: ${params.SOCIAL_MEDIA}")
        echo ("Password: ${params.SECRET}")
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

      input {
        message "Confirm to deplay?"
        ok "Yes, confirm!"
        submitter "vincent, rachel"
        parameters {
          choice (name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: "Select deploy area")
        }
      }

      steps {
        echo "Deployed to ${TARGET_ENV}"
      }
    }

    stage('Release') {
      agent {
        node {
          label "linux && java17"
        }
      }

      when {
        expression{
          return params.DEPLOY
        }
      }

      steps {
        echo ("Release to User")
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