pipeline {
    agent any

    environment {
        WEB_DIR = "/var/www/html"
        SRC_DIR = "Sample_website"   // folder in your repo where files are located
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Pulling latest code from GitHub...'
                git branch: 'main', url: 'https://github.com/Raja4123/My_Projects.git'
            }
        }

        stage('Deploy to Nginx') {
            steps {
                echo 'Deploying only website folder to Nginx...'
                sh '''
                    sudo rm -rf ${WEB_DIR}/*
                    sudo cp -r ${SRC_DIR}/* ${WEB_DIR}/
                    sudo systemctl restart nginx
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
