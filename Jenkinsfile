pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'kiranss499@gmail.com', url: 'https://github.com/kirankiler9908/spring-boot-hello-world/'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("your-image-name:${env.BUILD_ID}", "-f Dockerfile .")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/', 'kiranss499@gmail.com') {
                        docker.image("your-image-name:${env.BUILD_ID}").push()
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
