pipeline {
    agent any

    stages {
        stage('Initial cleanup') {
            steps {
                script {
                    dir("${WORKSPACE}") {
                        deleteDir()
                    }
                }
            }
        }

        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/William-eng/php-todo.git'
            }
        }

        stage('Prepare Dependencies') {
            steps {
                sh 'mv .env.sample .env'
                sh 'composer install'
                sh 'php artisan migrate'
                sh 'php artisan db:seed'
                sh 'php artisan key:generate'
            }
        }

       stage('Execute Unit Tests') {
            steps {
                // Running PHPUnit tests
                sh './vendor/bin/phpunit'
            }
        }  
    }
    

}
