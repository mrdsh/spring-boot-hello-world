pipeline {
    agent any
    stages {
        stage('BUILD') {
            steps {
                echo "BUilding...."
                sh "export JAVA_HOME=/usr/java;mvn clean package -DskipTests=True"
            }
        }
    }
}