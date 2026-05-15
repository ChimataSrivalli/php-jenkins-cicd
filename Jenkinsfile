pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html/phpapp"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning GitHub Repo..."
                git branch: 'main', url: 'git@github.com:ChimataSrivalli/php-jenkins-cicd.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing composer dependencies..."
                sh '''
                    composer install --no-interaction
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                echo "Running PHPUnit tests..."
                sh '''
                    ./vendor/bin/phpunit --testdox
                '''
            }
        }

        stage('Deploy to Apache') {
            steps {
                echo "Deploying application to Apache folder..."
                sh '''
                    sudo rm -rf ${DEPLOY_DIR}/*
                    sudo cp -r * ${DEPLOY_DIR}/
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Pipeline Failed!"
        }
    }
}
