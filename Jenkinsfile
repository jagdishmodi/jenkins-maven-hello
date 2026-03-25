
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/jagdishmodi/jenkins-maven-hello.git',
                    branch: 'main'
            }
        }
    }
}
