pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'your-git-credentials-id', url: 'https://github.com/your/repository.git'
            }
        }

        stage('Build Spring Boot Application') {
            steps {
                // Example assuming Maven is installed globally on the Jenkins agent
                sh 'mvn clean package'  // Adjust Maven command as per your project
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image using the JAR file from the Spring Boot build
                    docker.build("your-image-name:${env.BUILD_ID}", "-f Dockerfile .")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://your-docker-registry', 'your-docker-credentials-id') {
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
