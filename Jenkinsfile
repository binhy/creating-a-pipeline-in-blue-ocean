pipeline {
  agent {
    docker {
      args '-p 3000:3000'
      image 'node:12-alpine'
    }

  }
  stages {
    stage('build') {
      steps {
        sh '''

yarn config set registry https://registry.npm.taobao.org -g
'''
        sh '''
yarn config set sass_binary_site http://cdn.npm.taobao.org/dist/node-sass -g




'''
        sh 'yarn install'
      }
    }

    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
  environment {
    CI = 'true'
  }
}