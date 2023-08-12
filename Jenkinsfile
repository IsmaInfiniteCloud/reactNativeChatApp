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

  }
}