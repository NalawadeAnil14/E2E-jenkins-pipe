pipeline {
    agent { label 'NODE1' }
    stages{
        stage("Checkout code"){
            steps{
                git branch: 'main', url: 'https://github.com/NalawadeAnil14/E2E-jenkins-pipe.git'
            }
        }
    }
}
