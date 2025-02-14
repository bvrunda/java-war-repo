pipeline {
    agent any
        stage('Parallel Execution') {
            parallel {
                stage ('checkout') {
                    steps {
                        echo 'this is for the test purpose'
                    }
                }
                stage('Build') {
                    steps {
                        echo 'Building the project...'
                        sh 'mvn clean install'
                    }
                }
               
            }
        }
    }
}
