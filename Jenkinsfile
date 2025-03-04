pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1' 
        ECR_REPO = '108782100023.dkr.ecr.us-east-1.amazonaws.com/vrunda'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Sandhyachinnu26/java-war-repo.git'
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
                    aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_REPO}
                    """

                    sh """
                    docker tag vrunda:latest 108782100023.dkr.ecr.us-east-1.amazonaws.com/vrunda:latest
                    """

                    sh """
                    docker push 108782100023.dkr.ecr.us-east-1.amazonaws.com/vrunda:latest
                    """
                }
            }
        }
    }
}
