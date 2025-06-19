pipeline {
    agent any

    environment {
        IMAGE_NAME = "sohit007/flaskapp"  // ✅ Use correct DockerHub username
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning repository...'
                sh '''
                    rm -rf myapp-jenkins-task
                    git clone https://github.com/Sohitmishra007/myapp-jenkins-task.git
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t $IMAGE_NAME ./myapp-jenkins-task"
            }
        }

        stage('Push') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // 🛠️ Add deployment logic here (SSH, Docker run, K8s, etc.)
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
