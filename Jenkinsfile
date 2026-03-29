pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'jdk21'
    }

    environment {
        APP_NAME = "hello-world-app"
        DOCKER_IMAGE = "hello-world-image"
        DOCKER_CONTAINER = "hello-world-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/jagdishmodi/hello-world-new.git', branch: 'master'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker rm -f $DOCKER_CONTAINER || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker run -d -p 8081:8080 --name $DOCKER_CONTAINER $DOCKER_IMAGE
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Pipeline Failed!'
        }
    }
}
