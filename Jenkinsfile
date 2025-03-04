pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1' 
        ECR_REPO = '108782100023.dkr.ecr.us-east-1.amazonaws.com/vrunda'
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
                sh "docker build -t vrunda ."
            }
        }

        stage('Push Image to AWS ECR') {
    steps {
        script {
            sh "aws configure set aws_access_key_id AKIARSU7LDY3XJQMJRVO"
            sh "aws configure set aws_secret_access_key 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"
            sh "aws configure set region ${AWS_REGION}"
            
            sh "aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_REPO}"
            sh "docker tag vrunda:latest ${ECR_REPO}:latest"
            sh "docker push ${ECR_REPO}:latest"
        }
    }
}

    }
}
