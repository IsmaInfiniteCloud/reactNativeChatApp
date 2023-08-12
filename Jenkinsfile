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
                sh 'npm ci'
            }
        }

        stage('Linting') {
            steps {
                sh 'npm run lint'
            }
        }

        stage('TypeScript Compilation') {
            steps {
                script {
                    // Check if TypeScript is installed
                    def hasTypeScript = sh(script: 'npm list typescript', returnStatus: true) == 0
                    if (!hasTypeScript) {
                        sh 'npm install typescript'
                    }
                }
                sh './node_modules/.bin/tsc --noEmit'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
            post {
                always {
                    junit '**/test-results.xml'
                }
            }
        }

        stage('Build Project') {
            steps {
                sh 'npm run build'
            }
        }
    }

    post {
        failure {
            mail to: 'team@example.com',
                 subject: 'Build Failed',
                 body: 'Check Jenkins for details.'
        }
    }
}
