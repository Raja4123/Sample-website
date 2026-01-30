pipeline {
    agent any
    environment{
        WEB_DIR = "/var/www/html/"
        BACKUP_DIR = "/var/backups/nginx"
    }

    stages {
        stage('cloning the code') {
            steps {
                git branch: 'main', url: 'https://github.com/Raja4123/Sample-website.git'
            }
        }
        stage('Backup Current Website') {
            steps {
                sh '''
                echo "Taking backup of current website..."
                TIMESTAMP=$(date +%F-%H-%M-%S)
                sudo mkdir -p $BACKUP_DIR/$TIMESTAMP
                sudo cp -r $WEB_DIR/* $BACKUP_DIR/$TIMESTAMP/ || true
                '''
            }
        }
        stage('Deploy new code') {
            steps {
                echo "Deploying new website..."
              sh  ''' 
                    sudo rm -rf $WEB_DIR/* 
                    sudo cp index.html style.css script.js $WEB_DIR/
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
            echo "Deployment failed! Rolling back..."

            sh '''
            LAST_BACKUP=$(ls -td $BACKUP_DIR/* | head -1)
            sudo rm -rf $WEB_DIR/*
            sudo cp -r $LAST_BACKUP/* $WEB_DIR/
            sudo systemctl restart nginx
            '''

            echo "Rollback completed successfully!"
        } 
    }
}
