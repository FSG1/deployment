pipeline {
    agent any

    stages {
        stage ('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Pull Images') {
            steps {
                sh 'docker-compose pull frontend backend'
            }
        }

        stage('Recreate Backend') {
            steps {
                sh 'docker-compose up -d backend'
            }
        }

        stage('Recreate Frontend') {
            steps {
                sh 'docker-compose up-d frontend'
            }
        }
    }
}
