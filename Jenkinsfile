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
                sh "mvn clean install"
            }
        }

        stage('Test') {
            steps {
                sh "mvn test"
            }
        }

        stage('Deployment') {
            parallel {
                stage('Deploy in Dev1') {
                    environment {
                        targer_user="ec2-user"
                        target_server="172.31.95.224"
                    }
                    steps {
                        sshagent(['cd-ssh-key']) {
                            sh 'scp -o StrictHostKeyChecking=no target/my-app-1.0-SNAPSHOT.jar $target_user@$target_server:/home/ec2-user'
                        }

                    }
                }

                stage('Deploy in Dev2') {
                    environment {
                        targer_user="ec2-user"
                        target_server="172.31.85.248"
                    }
                    steps {
                        sshagent(['cd-ssh-key']) {
                            sh 'scp -o StrictHostKeyChecking=no target/my-app-1.0-SNAPSHOT.jar $target_user@$target_server:/home/ec2-user'
                        }
                    }
                }
            }
        }

        stage('Deploy to UAT') {
            
                input {
                    message 'Do You want to Deploy in UAT ?'
                }
                
                steps {
                    echo "Awaiting"
                }

            }
            
        }
    }

    post {
        always {
            deleteDir()
        }

        failure {
            echo "The Maven job is Failed"
        }

        success {
            echo "The Job is successfully"
        }
    }
}
