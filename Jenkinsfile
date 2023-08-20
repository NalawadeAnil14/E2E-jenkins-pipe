pipeline {
    agent { label 'NODE1' }

    options {
       buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    environment {
       build_user = "${env.BUILD_USER}"
    }

    stages{
        stage("Checkout code") {
            steps {
                git branch: 'main', url: 'https://github.com/NalawadeAnil14/E2E-jenkins-pipe.git'
            }
        }

        stage("Unit testing") {
            steps {
                sh 'mvn test'
            }
        }

        stage("Integration testing") {
            steps {
               sh 'mvn verify -DskipUnitTests'
            }   
        }   

        stage("Build code") {
            steps {
                sh 'mvn clean install'
            }
        }

        stage("Docker build") {
            steps {
                //sh 'printenv'
                script {
                  sh 'docker build -t $JOB_NAME:v1.$BUILD_ID .'
                  sh 'docker tag $JOB_NAME:v1.$BUILD_ID anilnalawade/$JOB_NAME:v1.$BUILD_ID'
                  sh 'docker tag $JOB_NAME:v1.$BUILD_ID anilnalawade/$JOB_NAME:latest'
                }
            }
        }

        stage("Push docker image on dockerhub") {
            steps {
              script {
                withCredentials([usernamePassword(credentialsId: 'dockerhubToken', passwordVariable: 'dockerhub_password', usernameVariable: 'dockerhub_username')]) {
                  sh 'docker login -u ${dockerhub_username} -p ${dockerhub_password}'
                  sh 'docker push anilnalawade/$JOB_NAME:v1.$BUILD_ID'
                  sh 'docker push anilnalawade/$JOB_NAME:latest'
                }
              }  
           }  
       }     
   }
}   
