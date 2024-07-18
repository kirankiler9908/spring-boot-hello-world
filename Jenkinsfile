pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/kirankiler9908/spring-boot-hello-world'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("spring-app")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://your-docker-registry', 'docker-credentials-id') {
                        docker.image("spring-app").push()
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
