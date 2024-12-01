pipeline {
    agent any
    tools {
        nodejs 'NodeJs' // Ensure "NodeJs" matches the name configured in Jenkins -> Manage Jenkins -> Global Tool Configuration
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                // Installs project dependencies
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                // Runs the tests, allowing empty test suites to pass
                bat 'npm test -- --passWithNoTests'
            }
        }
    }
}
