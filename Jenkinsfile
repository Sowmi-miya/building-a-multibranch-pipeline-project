pipeline {
    agent any
    tools {
        nodejs 'NodeJS' // Ensure this matches the NodeJS installation in Jenkins
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
        stage('Deliver for development') {
            when {
                branch 'development'  // Execute only when the branch is 'development'
            }
            steps {
                echo 'Delivering for development...'
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./jenkins/scripts/deliver-for-development.sh'
                timeout(time: 5, unit: 'MINUTES') {
                    input message: 'Finished using the website? (Click "Proceed" to continue)'
                }
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'  // Execute only when the branch is 'production'
            }
            steps {
                echo 'Deploying for production...'
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./jenkins/scripts/deploy-for-production.sh'
                timeout(time: 5, unit: 'MINUTES') {
                    input message: 'Finished using the website? (Click "Proceed" to continue)'
                }
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./jenkins/scripts/kill.sh'
            }
        }
    }
}