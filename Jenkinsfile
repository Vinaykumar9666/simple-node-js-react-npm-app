pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh 'chmod -R +x  ./jenkins/scripts/test.sh'
        sh 'sh ./jenkins/scripts/test.sh '
      }
    }

    stage('Deliver') {
      steps {
        sh 'chmod -R +x ./jenkins/scripts/deliver.sh'
        sh 'sh ./jenkins/scripts/deliver.sh '
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh 'chmod -R +x ./jenkins/scrips/kill.sh'
        sh 'sh ./jenkins/scripts/kill.sh'
      }
    }

  }
  environment {
    CI = 'true'
  }
}