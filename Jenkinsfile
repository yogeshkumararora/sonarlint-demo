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
        /*stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }*/
        stage("SonarQube Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    script{
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }
    }
}
