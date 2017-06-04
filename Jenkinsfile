pipeline {
  agent any
  stages {
    stage('Checkout File') {
      steps {
        sh '''rm -rf *
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
            sh 'cat test-checkout/jenkins/sources'
            sleep 3
            
          },
          "Read Readme": {
            sh 'cat test-checkout/jenkins/README.md'
            catchError() {
              sh 'echo "123"'
            }
            input(message: 'Please click proceed for approval', id: 'approval_flag')
            
          }
        )
      }
    }
    stage('Next Stage 1') {
      steps {
        waitUntil() {
          fileExists 'test-checkout/test.txt'
        }
      }
    }
    stage('Next Stage 2') {
        try {
            sh 'exit 1'
        }
        catch (exc) {
            echo 'Something failed, I should sound the klaxons!'
            exit 0
        }  
    }
  }
  post { 
    always { 
        echo 'I will always say Hello again!'
    }
  }
}
