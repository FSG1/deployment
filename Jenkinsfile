pipeline {
    agent any

    stages {
        stage ('Checkout') {
            steps {
                checkout scm
            }
        }

        stage ('Stop Services') {
          steps {
            sh 'docker-compose -p fmms stop backend frontend'
          }
        }

        stage ('Build Projects') {
          parallel {
            stage ('Backend') {
              steps {
                build job: '../backend/master', wait: true
              }
            }

            stage ('Frontend') {
              steps {
                build job: '../frontend/master', wait: true
              }
            }
          }
        }

        stage('Start Backend') {
            steps {
                sh 'docker-compose -p fmms pull backend'
                sh 'docker-compose -p fmms up -d backend'
            }
        }

        stage('Start Frontend') {
            steps {
                sh 'docker-compose -p fmms pull frontend'
                sh 'docker-compose -p fmms up -d frontend'
            }
        }
    }
}
