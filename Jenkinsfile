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
        git(url: 'git@github.com:rudyk88/jenkins.git', branch: 'master', credentialsId: '0024186810b08b45bb23e89d6db69ae80430c291')
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
            
          }
        )
      }
    }
  }
}