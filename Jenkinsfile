pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('efaf09-dockerhub')
    }
    stages { 
        stage('GIT') {
            steps{
            git branch: 'main', url: 'https://github.com/efaf09/LaboratorioCICD.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t efaf09/labjenkins:latest .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push efaf09/labjenkins:latest'
            }
        }
    }
post {
        always {
            sh 'docker logout'
        }
    }
}
