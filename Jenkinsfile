pipeline {
        agent any
    environment {
        CONTAINER_NAME = 'nestjs-app'
        IMAGE_NAME = 'nestjs-image'
        PORT = '3000'
    }

    stages {
        stage('Clone the Repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/mohsinakhtaralam/cicd-pipeline-aws-ec2-docker-jenkins-github-webhook.git',
            }
        }

        stage('Build DDocker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Stop and remove existing container') {
            steps {
                sh """
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                """
            }
        }

        stage('Docker Container Run') {
            steps {
                sh """
                docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $IMAGE_NAME                """
            }
        }

      
    }
}