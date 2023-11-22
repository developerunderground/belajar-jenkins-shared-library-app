pipeline {
  agent none
  environment {
    AUTHOR = "Taruna Wahyudi"
    EMAIL = "wahyuditaruna97@gmail.com"
  }

  // triggers {
  //   cron("*/5 * * * *")
  //   pollSCM("*/5 * * * *")
  // }

  parameters {
    string(name: "NAME", defaultValue: "Guest", description: "What is your name")
    text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
    booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
    choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media")
    password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
  }

  options {
    disableConcurrentBuilds()
    timeout(time: 10, unit: 'MINUTES')
  }

  stages {

    stage("OS Setup") {
      matrix {
        axes {
          axis {
            name "OS"
            values "linux", "windows", "mac"
          }
          axis {
            name "ARC"
            values "32", "64"
          }
        }

        excludes {
          exclude {
            axis {
              name "OS"
              values "mac"
            }
            axis {
              name "ARC"
              values "32"
            }
          }
        }

        stages {
          stage("OS Setup") {
            agent {
              node {
                label "linux && java11"
              }
            }

            steps {
              echo("Setup ${OS} ${ARC}")
            }
          }
        }
      }
    }

    stage("Preparation") {

      parallel {
        stage("Prepare Java") {

          agent {
            node {
              label "linux && java11"
            }
          }

          steps {
            echo("Prepare Java")
            sleep(5)
          }
        }

        stage("Prepare Maven") {
          
          agent {
            node {
              label "linux && java11"
            }
          }

          steps {
            echo("Prepare Maven")
            sleep(5)
          }
        }
      }
    }

    stage("Parameter") {
      agent {
        node {
          label "linux && java11"
        }
      }

      steps {
        echo "Hello ${params.NAME}!"
        echo "You description is ${params.DESCRIPTION}!"
        echo "Your social media is ${params.SOCIAL_MEDIA} user!"
        echo "Need to deploy ${params.DEPLOY} to deploy!"
        echo "You secret is ${params.SECRET}"
      }
    }

    stage("Prepare") {

      environment {
        APP = credentials("taruna_creds")
      }

      agent {
        node {
          label "linux && java11"
        }
      }

      steps {
        echo("Author ${AUTHOR}")
        echo("Email ${EMAIL}")
        echo("Start Job: ${env.JOB_NAME}")
        echo("Start Build: ${env.BUILD_NUMBER}")
        echo("Branch Name: ${env.BRANCH_NAME}")
        echo("App User: ${APP_USR}")
        echo("App Password: ${APP_PSW}")
        sh('echo "App Password : $APP_PSW" > "rahasia.txt" ')
      }
    }

    stage("Build") {

      agent {
        node {
          label "linux && java11"
        }
      }

      steps {

        script {
          for (int i = 0; i < 10; i++) {
            echo("Script ${i}")
          }
        }

        echo("Start Build")
        sh("./mvnw clean compile test-compile")
        echo("Finish Build")
      }
    }

    stage("Test") {

      agent {
        node {
          label "linux && java11"
        }
      }

      steps {

        script {
          def data = [
            "firstName" : "Taruna",
            "lastName" : "Wahyudi"
          ]

          writeJSON(file: "data.json", json: data)
        }

        echo("Start Test")
        sh("./mvnw test")
        echo("Finish Test")
      }
    }

    stage("Deploy") {

      input {
        message "Can we deploy?"
        ok "Yes, of course"
        submitter "tarunawahyudi"
        parameters {
          choice(name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: "Which Environment?")
        }
      }

      agent {
        node {
          label "linux && java11"
        }
      }

      steps {
        echo("Deploy to ${TARGET_ENV}")
      }
    }

    stage("Release") {

      when {
        expression {
          return params.DEPLOY
        }
      }

      agent {
        node {
          label "linux && java11"
        }
      }

      steps {
        withCredentials([usernamePassword(
          credentialsId: "taruna_creds",
          usernameVariable: "USER",
          passwordVariable: "PASSWORD"
        )]) {
          sh('echo "Release it with -u $USER -t $PASSWORD" > "release.txt"')
        }
      }
    }
  }

  post {
    always {
      echo "Gas dah bray jenkins nyaaa"
    }
    success {
      echo "MANTAP BERHASIL COOK!!"
    }
    failure {
      echo "Ya ampun amsyong cook error"
    }
    cleanup {
      echo "Dah beres nih build nya cuy"
    }
  }
}