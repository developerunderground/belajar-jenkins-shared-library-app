pipeline {
  agent {
    node {
      label "linux && java11"
    }
  }

  stages {
    stage("Build") {
      steps {
        echo("Hello Build")
      }
    }

    stage("Test") {
      steps {
        echo("Hello Test")
        sh("error")
      }
    }

    stage("Deploy") {
      steps {
        echo("Hello Deploy")
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