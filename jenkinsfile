pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning repository...'
                // Example: git 'https://github.com/Sohitmishra007/myapp-jenkins-task'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example: sh './build.sh'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Example: sh './run-tests.sh'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Example: sh './deploy.sh'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
