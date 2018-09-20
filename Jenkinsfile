pipeline {
  agent {
    docker {
      args '-p 3000:3000'
      image 'node:6-alpine'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh '''
npm install

'''
      }
    }
    stage('Deliver') {
      parallel {
        stage('Deliver') {
          steps {
            sh './jenkins/scripts/deliver.sh'
            input '<"Proceed" to Continue'
            sh './jenkins/scripts/kill.sh'
          }
        }
        stage('Test') {
          environment {
            CI = 'true'
          }
          steps {
            sh './jenkins/scripts/test.sh'
          }
        }
      }
    }
    stage('email') {
      steps {
        emailext(subject: 'This is a test', body: 'from BC ', from: 'indira', replyTo: 'indira.thangasamy@moogsoft.com', to: 'indira.thangasamy@moogsoft.com')
        mail(subject: 'indira', body: 'this is test', to: 'inthanga@gmail.com', replyTo: 'inthanga@gmail.com', from: 'inthanga@gmail.com', cc: 'inthanga@gmail.com')
      }
    }
    stage('Validate') {
      steps {
        timestamps()
      }
    }
  }
}