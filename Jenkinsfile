pipeline {
  agent any
  stages {
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
      steps {
        sh 'echo "XYZ"'
      }
    }
  }
  environment {
    Server = 'Centos'
    Environment = 'DEV'
  }
  post {
    always {
      echo 'I will always say Hello again!'
      
    }
    
  }
}