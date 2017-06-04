pipeline {
  agent any
  stages {
    stage('Checkout File') {
      steps {
        sh '''rm -rf test-checkout
mkdir -p test-checkout
cd test-checkout
touch test.txt
git clone git@github.com:rudyk88/jenkins.git'''
      }
    }
    stage('Read File') {
      steps {
        parallel(
          "Read File": {
            sh 'cat sources'
            
          },
          "Read Readme": {
            sh 'cat jenkins/readme.md'
            
          }
        )
      }
    }
  }
}