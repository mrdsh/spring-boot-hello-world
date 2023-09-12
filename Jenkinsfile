pipeline {
    agent any
    stages {
        stage('BUILD') {
            steps {
                echo "BUilding...."
                bash "mvn clean package -DskipTests=True"
            }
        }
    }
}