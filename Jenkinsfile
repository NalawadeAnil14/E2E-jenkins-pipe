pipeline {
    agent { label 'NODE1' }

    options {
       buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    stages{
        stage("Checkout code"){
            steps{
                git branch: 'main', url: 'https://github.com/NalawadeAnil14/E2E-jenkins-pipe.git'
            }
        }

        stage("Unit testing"){
            steps {
                sh 'mvn test'
            }
        }

        stage("Integration testing")
           steps{
            sh 'mvn verify -DskipUnitTests'
           }   
    }   
}
