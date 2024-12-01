pipeline {
    agent any
    tools {
        nodejs 'NodeJS' // Ensure this matches the exact name in Jenkins configuration
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                bat 'npm test -- --passWithNoTests'
            }
        }
    }
}
