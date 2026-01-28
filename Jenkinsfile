pipeline {
    agent any

    stages {
        stage('cloning the code') {
            steps {
                git branch: 'main', url: 'https://github.com/Raja4123/Sample-website.git'
            }
        }
        stage('copy the code to nginx') {
            steps {
              sh  ''' 
                    sudo rm -rf /var/www/html/* 
                    sudo cp index.html style.css script.js /var/www/html/
                '''
            }
        }
        stage('restart the nginx') {
            steps {
              sh 'sudo systemctl restart nginx'
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
