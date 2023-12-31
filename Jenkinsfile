def APP_NAME = "spring-boot-hello-world"

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
                    def BUILD_NUM = env.BUILD_ID
                    sh "cd kube_file && kustomize   edit set image ${APP_NAME}:${env.BUILD_ID}"
                    withKubeConfig([credentialsId: 'kube_config']) {
                        sh "kubectl apply -n my-apps -k kube_file"
                    }
                }
            }
        }
    }
}