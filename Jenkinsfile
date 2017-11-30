pipeline {
    agent any

    stages {
        stage ('Checkout') {
            steps {
                checkout scm
            }
        }

        if (env.BRANCH_NAME == "master") {
          stage ('Build Backend') {
            steps {
              build job: '../backend/master', wait: true
            }
          }

          stage ('Build Frontend') {
            steps {
              build job: '../frontend/master', wait: true
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
