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
                dir('src) {  // Change to your Spring Boot app directory
                    sh './mvnw clean package'  // Adjust Maven command as per your project
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("kiran:${env.BUILD_ID}", "-f Dockerfile .")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/', 'kiranss499@gmail.com') {
                        docker.image("kiran:${env.BUILD_ID}").push()
                    }
                }
            }
        }
    }

 //   post {
    //    always {
          //  cleanWs()
    //    }
 //   }
}
