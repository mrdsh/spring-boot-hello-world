pipeline {
    agent any
    stages {
        stage('BUILD') {
            steps {
                echo "BUilding...."
                sh "mvn clean package -DskipTests=True"
            }
        }
    }
}