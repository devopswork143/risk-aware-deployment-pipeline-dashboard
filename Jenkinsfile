
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code'
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

        stage('Docker Build') {
            steps {
                sh 'docker build -t risk-aware-dashboard:${BUILD_NUMBER} .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh '''
                    docker rm -f risk-aware-dashboard || true

                    docker run -d \
                    --name risk-aware-dashboard \
                    --restart unless-stopped \
                    -p 3000:3000 \
                    risk-aware-dashboard:${BUILD_NUMBER}
                '''
            }
        }
    }

    post {
        success {
            echo 'Docker application deployed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Jenkins console output.'
        }
    }
}
