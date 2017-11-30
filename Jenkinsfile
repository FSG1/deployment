def branches = [:]
branches["backend"] = {
  build job: '../backend/master', wait: true
}

branches["frontend"] = {
  build job: '../frontend/master', wait: true
}

pipeline {
    agent any

    stages {
        stage ('Checkout') {
            steps {
                checkout scm
            }
        }

        stage ('Build Backend & Frontend') {
            steps {
              parallel branches
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
