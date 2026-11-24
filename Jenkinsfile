
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out Risk-Aware Deployment Pipeline'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Lint') {
            steps {
                sh 'npm run lint'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
    }

    post {
        success {
            echo 'Project built successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
