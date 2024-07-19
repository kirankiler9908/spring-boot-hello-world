
pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'kiranss499@gmail.com', url: 'https://github.com/kirankiler9908/spring-boot-hello-world/'
                  sh 'ls -la'
            }
        }
       stage('Build Spring Boot Application') {
            steps {
                
                    sh 'mvn clean install'  // Adjust Maven command as per your project
               
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("killer9908/kiran:${env.BUILD_ID}", "-f Dockerfile .")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub') {
                        docker.image("killer9908/kiran:${env.BUILD_ID}").push()
                    }
                }
            }
        }
    }

 // post {
 //    always {
 //         cleanWs()
//       }
//  }
}
