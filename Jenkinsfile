pipeline {
    agent any
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
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "chmod +x ./jenkins/scripts/test.sh && ./jenkins/scripts/test.sh"'
            }
        }
        stage('Deliver for Development') {
            when {
                branch 'development'
            }
            steps {
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "./jenkins/scripts/deliver-for-development.sh"'
                input message: 'Finished using the website? (Click "Proceed" to continue)'
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "./jenkins/scripts/kill.sh"'
            }
        }
        stage('Deploy for Production') {
            when {
                branch 'production'
            }
            steps {
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "./jenkins/scripts/deploy-for-production.sh"'
                input message: 'Finished using the website? (Click "Proceed" to continue)'
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "./jenkins/scripts/kill.sh"'
            }
        }
    }
}
