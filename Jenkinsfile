pipeline {
    agent any

    environment {
        WEB_DIR = "/var/www/html"
        BACKUP_DIR = "/var/backups/nginx"
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Raja4123/Sample-website.git'
            }
        }

        stage('Backup Current Website') {
            steps {
                sh '''
                mkdir -p $BACKUP_DIR
                TIMESTAMP=$(date +%F-%H-%M-%S)
                mkdir -p $BACKUP_DIR/$TIMESTAMP
                cp -r $WEB_DIR/* $BACKUP_DIR/$TIMESTAMP/ || true
                '''
            }
        }

        stage('Deploy New Code') {
            steps {
                sh '''
                rm -rf $WEB_DIR/*
                cp index.html style.css script.js $WEB_DIR/
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
        failure {
            echo "Deployment failed. Rolling back..."
            sh '''
            LAST_BACKUP=$(ls -td $BACKUP_DIR/* | head -1)
            rm -rf $WEB_DIR/*
            cp -r $LAST_BACKUP/* $WEB_DIR/
            systemctl restart nginx
            '''
        }
    }
}
