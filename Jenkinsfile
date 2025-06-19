pipeline {
  agent any
  environment {
    IMAGE_NAME = 'sohitmishra/flaskapp'
  }
  stages {
    stage('Clone Repo') {
      steps {
        echo 'Cloning repository...'
        sh 'git clone https://github.com/Sohitmishra007/myapp-jenkins-task.git'
      }
    }
    stage('Build') {
      steps {
        echo 'Building Docker image...'
        sh 'docker build -t $IMAGE_NAME ./myapp-jenkins-task'
      }
    }
    stage('Push') {
      steps {
        echo 'Pushing Docker image...'
        withCredentials([usernamePassword(
          credentialsId: '8caf46a2-d6eb-46d0-aa28-d2a91fd2fa34',
          usernameVariable: 'DOCKER_USER',
          passwordVariable: 'DOCKER_PASS'
        )]) {
          sh '''
            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
            docker push $IMAGE_NAME
          '''
        }
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying to VM...'
        sshagent(['7219a01a-3ec9-451c-9d80-da0d695ff845']) {
          sh "ssh -o StrictHostKeyChecking=no sohit_mishra@34.93.181.160 'docker pull $IMAGE_NAME && docker stop flaskapp || true && docker rm flaskapp || true && docker run -d --name flaskapp -p 80:5000 $IMAGE_NAME'"
        }
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
