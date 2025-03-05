pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1c' 
        ECR_REPO = '108782100023.dkr.ecr.us-east-1c.amazonaws.com/new_repo'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/bvrunda/java-war-repo.git'
            }
        }

        stage('Build Java Application') {
            steps {
                sh 'mvn clean package -DskipTests' 
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t new_repo ."
            }
        }

        stage('Push Image to AWS ECR') {
    steps {
        script {
            
            sh "aws ecr get-login-password --region ${AWS_REGION} | sudo docker login --username AWS --password-stdin ${ECR_REPO}"
            sh " sudo docker tag new_repo:latest ${ECR_REPO}:latest"
            sh "sudo docker push ${ECR_REPO}:latest"
        }
    }
}

    }
}
