pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    stages {
        stage('Sonarqube') {
            environment {
                scannerHome = tool 'SonarScanner'
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    bat 'mvn clean package sonar:sonar'
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
        }
}
    }
    post {
        always {
            junit(
                allowEmptyResults: true, 
                testResults: '**/build/test-results/test/*.xml'
            )
            recordIssues(
                enabledForFailure: true, aggregatingResults: true,
                tools: [java(), checkStyle()]
            )
        }
    }
}
