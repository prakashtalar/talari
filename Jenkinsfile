pipeline {
    agent any
    environment {
        registry = "975295541129.dkr.ecr.us-east-1.amazonaws.com/myecr1"
        dockerImageTag = "1.0" // Specify your desired tag here
    }
    stages {
        stage('Code Checkout') {
            steps {
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'c9f3b495-e17a-4938-895f-a19a364cc3a9', url: 'https://github.com/prakashtalar/masterjnks.git']])
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${dockerImageTag}")
                }
            }
        }
        stage('Pushing to ECR') {
            steps {
                script {
                    sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 975295541129.dkr.ecr.us-east-1.amazonaws.com'
                    sh "docker push ${registry}:${dockerImageTag}"
                }
            }
        }
    }
}
