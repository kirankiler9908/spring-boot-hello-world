pipeline {
    agent {
        docker {
            image 'maven:3.8.4-openjdk-11'
            args '-v /root/.m2:/root/.m2'  // Optional: Mount Maven cache volume for faster builds
        }
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'kiranss499@gmail.com', url: 'https://github.com/kirankiler9908/spring-boot-hello-world/'
                  sh 'ls -la'
            }
        }
       stage('Build Spring Boot Application') {
            steps {
                dir('src') {  // Change to your Spring Boot app directory
                    sh 'mvn clean install'  // Adjust Maven command as per your project
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
