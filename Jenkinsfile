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
             sh "mvn clean install"
          }
      }

      stage('Print ENV') {
          environment {
              myVar="T.Gangireddy"
          }
          steps {
             sh 'echo "====My Name is :$myVar and Ganga++++===="'
          }
      }


    }

}
