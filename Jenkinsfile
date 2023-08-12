pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // This checks out the code from your repository
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Lint Codebase') {
            steps {
                sh 'npm run lint'
            }
        }

        stage('Run TypeScript Compiler') {
            steps {
                sh 'npm run tsc'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm run test'
            }
        }
        
        // You can add more stages as necessary. For instance, if you have deployment steps, they would go here.

    }
}
