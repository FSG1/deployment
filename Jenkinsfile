pipeline {
    agent any

    stages {
        stage ('Checkout') {
            steps {
                checkout scm
                echo env.BRANCH_NAME
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
