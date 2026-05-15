pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git credentialsId: 'github-ssh-key',
                    url: 'git@github.com:ChimataSrivalli/php-jenkins-cicd.git',
                    branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    pwd
                    ls -la
                    composer install --no-interaction
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                    pwd
                    ls -la
                    ./vendor/bin/phpunit --testdox tests
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    sudo cp -r * /var/www/html/phpapp/
                '''
            }
        }
    }
}
