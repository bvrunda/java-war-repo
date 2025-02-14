pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo.git'
            }
        }
        stage('Parallel Execution') {
            parallel {
                stage('Build') {
                    steps {
                        echo 'Building the project...'
                        // Example: mvn package or npm install
                    }
                }
                stage('Test') {
                    steps {
                        echo 'Running tests...'
                        // Example: mvn test or pytest
                    }
                }
            }
        }
    }
}
