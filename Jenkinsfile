pipeline {
    agent any
    stages {
        stage('BUILD') {
            agent { docker 'maven:3.9.3-eclipse-temurin-17' }
            steps {
                echo "Building...."
                sh "mvn clean package -DskipTests=True"
            }
        }
    }
}