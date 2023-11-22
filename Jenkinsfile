@Library("belajar-jenkins-shared-library@main") _

import stacklabdeveloper.jenkins.Output

pipeline {
  agent any
  stages {

    stage("Hello Grovy") {
      steps {
        script {
          Output.hello(this, "Groovy")
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
  }
}