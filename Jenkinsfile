pipeline {
    agent any

    stages {
        stage ('Checkout') {
            steps {
                checkout scm
            }
        }

        stage ('Build Backend & Frontend') {
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

        stage('Pull Images') {
            steps {
                sh 'docker-compose -p fmms pull frontend backend'
            }
        }

        stage('Recreate Backend') {
            steps {
                sh 'docker-compose -p fmms up -d backend'
            }
        }

        stage('Recreate Frontend') {
            steps {
                sh 'docker-compose -p fmms up -d frontend'
            }
        }
    }
}
