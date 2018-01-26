pipeline {
    agent any

    tools {
        maven 'M3'
        jdk 'Java8'
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'c069cc77-ef5a-4fca-9c15-5997070066b8', url: 'https://github.com/yogeshkumararora/sonarlint-demo.git'
            }
        }
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube Scan') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }
    }
}