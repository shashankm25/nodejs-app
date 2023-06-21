pipeline {
    agent {label "Slave-Docker"} 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('mshashank')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git branch: 'main' , url: 'https://github.com/shashankm25/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t mshashank/nodeapp:tag number 2 .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push mshashank/nodeapp:tag number 2'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
