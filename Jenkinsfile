pipeline {
    agent any

    

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/jagdishmodi/jenkins-maven-hello.git',
                   
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -B clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn -B test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                sh 'mvn -B package'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }

        stage('Execute HelloWorld') {
            steps {
                sh 'java -cp target/helloworld-1.0-SNAPSHOT.jar com.example.HelloWorld'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}

