pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Linting') {
            steps {
                sh 'npm run lint'
            }
        }

        stage('TypeScript Compilation') {
            steps {
                sh './node_modules/.bin/tsc --noEmit'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Project') {
            steps {
                sh 'npm run build'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/lib/**', allowEmptyArchive: true
        }
    }
}
