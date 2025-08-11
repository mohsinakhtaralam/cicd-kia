pipeline {
    agent any
    environment {
        CONTAINER_NAME = 'nestjs-app'
        IMAGE_NAME = 'nestjs-image'
        EMAIL = 'mdxb.info@gmail.com'
        PORT = '3000'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/mohsinakhtaralam/cicd-pipeline-aws-ec2-docker-jenkins-github-webhook'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('stop and remove existing container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Docker Container Run') {
            steps {
                sh '''
                docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $IMAGE_NAME 
                '''
            }
        }

        stage('Send Email') {
            steps {
                emailext(
                    to: "${EMAIL}",
                    subject: "Docker Deployment Successful",
                    body: "The Docker container for app at http://54.80.207.55:8080:${PORT}",
                )
            }
        }
    }
}