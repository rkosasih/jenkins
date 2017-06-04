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
        git(credentialsId: '26e9a944265540c962446c8305611ae4eb9e426c', url: 'ssh://git@github.com:rudyk88/jenkins.git', branch: 'master')
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
