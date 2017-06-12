pipeline {
  agent any
  stages {
    stage('Read File') {
      steps {
        parallel(
          "Read File": {
            sh 'echo "Hello World ..."'
            sleep 3
            sh '''if [ -f jenkins/sources ]; then
  cat jenkins/sources
else
  echo "Please provide the sources file"
fi'''
            
          },
          "Read Readme": {
            sh 'cat jenkins/README.md'
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
    server = 'Centos'
    environ = 'DEV'
  }
  post {
    always {
      echo 'I will always say Hello again!'
      
    }
    
  }
}