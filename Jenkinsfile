pipeline {
    agent {
        label 'agent1'
    }

    tools {
        maven 'maven3.6.3'
    }

    stages {
        stage('Checkout') {
            steps {
                 checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "mvn --version"
                sh "mvn clean package"
            }
        }

        stage('Test') {
            steps {
                sh "mvn test"
            }
        }

        stage('Print Env') {
            environment {
                myVar="GANGIREDDy"
            }
            steps {
               sh  'echo "MY NAME IS :$myVar"'
            }
        }

    }
}
