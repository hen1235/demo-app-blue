pipeline {
  agent any
  stages {
    stage('Restore') {
      steps {
        sh 'npm install'
      }
    }

    stage('Tests') {
      parallel {
        stage('Test 1') {
          steps {
            sh '''npm run test1
'''
          }
        }

        stage('Test 2') {
          steps {
            sh 'npm run test2'
          }
        }

        stage('Test 3') {
          steps {
            sh 'npm run test3'
          }
        }

      }
    }

    stage('Test Env') {
      agent {
        node {
          label 'Test'
        }

      }
      steps {
        sh 'docker-compose up -d --build'
      }
    }

    stage('Approval') {
      steps {
        input(message: 'Approve?', ok: 'Yes')
      }
    }

    stage('Prod Env') {
      agent {
        node {
          label 'Production'
        }

      }
      steps {
        sh 'docker-compose up -d --build'
      }
    }

  }
}