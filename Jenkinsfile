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
                script {
                    // Ensure the correct TypeScript and type definitions are installed
                    sh 'npm install'
                    sh 'npm install @types/react@latest @types/react-native@latest typescript@latest'
                }
            }
        }

        stage('Linting') {
            steps {
                script {
                    // Run linting
                    sh 'npm run lint'
                }
            }
        }

        stage('Type Checking') {
            steps {
                script {
                    // Run TypeScript compiler
                    try {
                        sh 'npm run tsc'
                    } catch (Exception e) {
                        echo 'TypeScript compilation failed!'
                        throw e
                    }
                }
            }
        }

        stage('Testing') {
            steps {
                script {
                    // Run tests
                    sh 'npm run test'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the project
                    sh 'npm run build'
                }
            }
        }
    }

    post {
        always {
            // Cleanup
            echo 'Cleaning up...'
            sh 'rm -rf node_modules'
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Something went wrong...'
        }
    }
}
