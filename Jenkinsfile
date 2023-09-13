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
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker_hub') {
                        def customImage = docker.build("mrdash/spring-boot-hello-world:${env.BUILD_ID}")
                        customImage.push()
                        customImage.push('latest')
                    }
                }
            }
        }
        stage('DEPLOY') {
            steps {
                script {
                    withKubeConfig([credentialsId: 'user1']) {
                        sh "kubectl get po"
                    }
                }
            }
        }
    }
}