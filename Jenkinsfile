pipeline {
  agent any
  stages {
    stage('Read File') {
      steps {
        parallel(
          "Stage 1": {
            sh 'echo "Hello World ..."'
            sleep 3
            sh '''if [ -f jenkins/sources ]; then
  cat jenkins/sources
else
  echo "Please provide the sources file"
fi'''
            
          },
          "Read Readme": {
            sh 'cat README.md'
            catchError() {
              sh 'echo "123"'
            }
            
            input(message: 'Please click proceed for approval', id: 'approval_flag')
            
          }
        )
      }
    }
    stage('Next Stage') {
      steps {
        sh '''touch test.txt
echo ${server} > test.json
echo ${environ} >> test.json
echo "---" >> test.json
echo ${DEV_ACCESS} >> test.json
echo ${dev_user} >> test.json
echo ${DEV_ACCESS_USR} >> test.json
echo ${DEV_ACCESS_PSW} >> test.json
'''
        waitUntil() {
          fileExists 'test.txt'
        }
        
      }
    }
    stage('Final Stage') {
      steps {
        sh '''echo "XYZ"

version="3.1.18"
cat << EOF > versions.json
{"version": $version}
EOF'''
        archiveArtifacts '*.json'
      }
    }
  }
  environment {
    server = 'Centos'
    environ = 'DEV'
    DEV_ACCESS = credentials('devuser')
  }
  post {
    always {
      echo 'I will always say Hello again!'
      
    }
    
  }
}
