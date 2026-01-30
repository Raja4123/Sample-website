pipeline {
    agent any


    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Raja4123/Sample-website.git'
            }
        }
        stage('Deploy New Code') {
            steps {
                sh '''
                rm -rf /var/www/html/*
                cp index.html style.css script.js /var/www/html/
                '''
            }
        }

        stage('Restart Nginx') {
            steps {
                sh 'systemctl restart nginx'
            }
        }
    }

    post {
        success{
            echo "pipeline completed successfully"
        }
        failure {
            echo "pipeline failed"            
        }
    }
}
