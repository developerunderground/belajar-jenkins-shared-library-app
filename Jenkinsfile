@Library("belajar-jenkins-shared-library@main") _

import stacklabdeveloper.jenkins.Output

pipeline {
  agent any
  stages {

    stage("Maven Build") {
      steps {
        script {
          maven("clean compile")
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