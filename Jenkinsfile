pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/bvrunda/java-war-repo'
            }
        }
        stage('Parallel Execution') {
            parallel {
                stage('Build') {
                    steps {
                        echo 'Building the project...'
                        sh 'mvn clean install
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
