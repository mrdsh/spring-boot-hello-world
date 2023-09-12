pipeline {
    agent any
    stages {
        stage('BUILD Package') {
            agent { 
                docker {
                    image 'maven:3.9.3-eclipse-temurin-17' 
                    reuseNode true
                }
            }
            steps {
                echo "Building Package...."
                sh "mvn clean package -DskipTests=True"
            }
        }
        stage('BUILD Image') {
            steps {
                echo "Building image...."
                sh "tree"
                script {
                    def customImage = docker.build("spring-boot-hello-world:${env.BUILD_ID}")
                    customImage.push()
                }
            }
        }
    }
}