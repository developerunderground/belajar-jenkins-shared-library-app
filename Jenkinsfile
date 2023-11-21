pipeline {
  agent {
    node {
      label "linux && java11"
    }
  }

  stages {
    stage("Hello") {
      steps {
        echo("Hello Pipeline")
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