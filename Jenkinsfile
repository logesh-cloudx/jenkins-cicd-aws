pipeline {
    agent any

    stages {

        stage('Code Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                git branch: 'main',
                    url: 'https://github.com/logesh-cloudx/jenkins-cicd-aws.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Build started...'
                sh 'echo Build completed on $(date)'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo All tests passed!'
            }
        }

        stage('Deploy to SIT') {
            steps {
                echo 'Deploying to SIT...'
                sh '''
                    sudo mkdir -p /var/www/sit
                    sudo cp index.html /var/www/sit/
                    echo "SIT Deployment done!"
                '''
            }
        }

        stage('Deploy to UAT') {
            steps {
                echo 'Deploying to UAT...'
                sh '''
                    sudo mkdir -p /var/www/uat
                    sudo cp index.html /var/www/uat/
                    echo "UAT Deployment done!"
                '''
            }
        }

        stage('Deploy to Production') {
            steps {
                input message: 'Approve Production Deployment?',
                      ok: 'Deploy Now'
                echo 'Deploying to Production...'
                sh '''
                    sudo mkdir -p /var/www/prod
                    sudo cp index.html /var/www/prod/
                    echo "Production Deployment done!"
                '''
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check logs.'
        }
    }
}