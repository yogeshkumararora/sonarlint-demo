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
        
        //Just run SonarQube
        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        //Check quality gates
        stage("SonarQube Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    script{
                        def qg = waitForQualityGate()
                        /*if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }*/
                        
                        if (qg.status == 'OK') {
                           // Input Step
                            timeout(time: 15, unit: "MINUTES") {
                                //def userInput = input(id: 'userInput', message: 'SonarQube Quality Gate is failing, do you still want to proceed?', ok: 'Yes')
                                //println ("userInput: $userInput");
                                
                                def feedback = input(submitterParameter: 'submitter', message: 'SonarQube Quality Gate is failing, do you still want to proceed?', ok: 'Yes')
                                echo "It was ${feedback.submitter} who submitted the dialog."
                            }
                        }
                    }
                }
            }
        }
    }
}
