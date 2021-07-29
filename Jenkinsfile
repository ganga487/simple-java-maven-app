pipeline {
    agent {
        label 'agent1'
    }

    tools {
        maven 'maven3.6.3'
    }

    options {
               timeout(10)
               buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '5')
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

        stage('Deployment') {
            steps {
                sshagent(['cd-ssh-key']) {
                     // some block
                      sh "scp -o StrictHostKeyChecking= no ec2-user@172.31.0.111:/home/ec2-user/sa.txt  ec2-user@172.31.95.224:/home/ec2-user/"
                }
            }
        }

    }
    post {
        always {
            deleteDir()
        }

        failure {
            echo "Sendmail -s Maven job failed receipt@mycompany.com"
        }

        success {
            echo "The job is successfully"
        }
    }
}
