pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1' 
        ECR_REPO = '108782100023.dkr.ecr.us-east-1.amazonaws.com/vrunda:latest'
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
                    sh """
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 108782100023.dkr.ecr.us-east-1.amazonaws.com
                    """

                    sh """
                    docker tag vrunda:latest ${ECR_REPO}:latest
                    """

                    sh """
                    docker push ${ECR_REPO}:latest
                    """
                }
            }
        }
    }
}
