pipeline {
    agent any

    environment {
        CONTAINER_NAME = "cicd"
        IMAGE_NAME = "cicd:latest"
        EMAIL = "abulalajobayar@gmail.com"
        PORT = "3000"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AbulAlaJobayar/-CI-CD-Pipeline-with-Jenkins-Docker-AWS-EC2-GitHub-Email-for-NestJS-App'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Docker container run') {
            steps {
                sh '''
                docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
        stage('Send Email'){
            steps {
                emailtext(
                    subject: 'Deployment Successful on EC2',
                    body: 'The application has been successfully deployed.http://13.53.235.252:3000',
                    to: "$EMAIL"
                )
            }
        }
    }
}