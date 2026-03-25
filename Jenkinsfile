pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/jagdishmodi/jenkins-maven-hello.git',
                    branch: 'main'
                )
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
