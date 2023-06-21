pipeline {
    agent {label "Slave-Docker"} 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-mshashank')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git branch: 'main' , url: 'https://github.com/shashankm25/nodejs-app.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t mshashank/nodeapp:$BUILD_NUMBER.'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push mshashank/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
