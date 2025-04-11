pipeline {
    agent any

    environment {
        STAGING_DIR = "C:\\deployments\\staging"
        PROD_DIR = "C:\\deployments\\production"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/jatin904/win-local-cicd.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the app...'
                bat 'echo Build successful > build.log'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'echo All tests passed > test.log'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                bat 'copy app.py "%STAGING_DIR%" /Y'
            }
        }

        stage('Approval for Production') {
            steps {
                input message: 'Approve to deploy to Production?'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                bat 'copy app.py "%PROD_DIR%" /Y'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed!'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}
