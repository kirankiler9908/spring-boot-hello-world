pipeline {
    agent any  // Use 'any' as the agent type

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('kiranss499@gmail.com')  // Credential ID for Docker Hub
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'kiranss499@gmail.com', url: 'https://github.com/kirankiler9908/spring-boot-hello-world.git'
                sh 'ls -la'  // Optional: List files in the cloned repository for verification
            }
        }

        stage('Build Spring Boot Application') {
            agent {
                docker {
                    image 'maven:3.8.4-openjdk-11'
                    args '-v /root/.m2:/root/.m2'  // Optional: Mount Maven cache volume for faster builds
                }
            }
            steps {
                dir('spring-boot-hello-world') {  // Adjust to your actual Spring Boot app directory
                    sh 'mvn clean install'  // Maven command to build the Spring Boot application
                }
            }
        }

        stage('Build Docker Image') {
            agent any  // Use 'any' as the agent type for this stage
            steps {
                script {
                    docker.build("kiran:${env.BUILD_ID}", "-f spring-boot-hello-world/Dockerfile .")
                }
            }
        }

        stage('Push Docker Image') {
            agent any  // Use 'any' as the agent type for this stage
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("kiran:${env.BUILD_ID}").push()
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
