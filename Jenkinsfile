pipeline {
    agent {
        label 'agent1'
    }
    //tools {
      //  maven 'mvn-3.8.1'
    //}
    stages {
      stage('Checkout') {
        steps {
            checkout scm
        }
     }
      stage('Build') {
          steps {
             sh "mvn clean install"
          }
      }

      stage('Print ENV') {
          environment {
              myVar="T.Gangireddy"
          }
          steps {
             sh 'echo "====My Name is :$myVar++++===="'
          }
      }


    }

}
