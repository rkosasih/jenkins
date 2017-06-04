pipeline {
  agent any
  stages {
    stage('Checkout File') {
      steps {
        sh 'git clone git@github.com:rudyk88/jenkins.git'
      }
    }
    stage('Read File') {
      steps {
        parallel(
          "Read File": {
            sh 'cat sources'
            
          },
          "Read Readme": {
            sh 'cat readme.md'
            
          }
        )
      }
    }
  }
}