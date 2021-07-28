pipeline {
    agent {
        label 'agent1'
    }
    stages {
      stage('Checkout') {
        steps {
            Checkout Scm
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
