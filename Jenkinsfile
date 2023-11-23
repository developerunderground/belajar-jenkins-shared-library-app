@Library("belajar-jenkins-shared-library@main") _

import stacklabdeveloper.jenkins.Output

pipeline {
  agent any
  stages {

    stage("Library Resources") {
      steps {
        script {
          def config = libraryResource("config/build.json")
          echo("config")
        }
      }
    }

    stage("Maven Build") {
      steps {
        script {
          maven(["clean", "compile", "test"])
        }
      }
    }

    stage("Global Variabel") {
      steps {
        script {
          echo(author())
          echo(author.name())
          echo(author.channel())
        }
      }
    }

    stage("Hello World") {
      steps {
        script {
          hello.world()
        }
      }
    }

    stage("Hello Grovy") {
      steps {
        script {
          Output.hello(this, "Groovy")
        }
      }
    }

  }
}