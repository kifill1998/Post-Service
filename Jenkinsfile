pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    stage('Sonarqube') {
    environment {
        scannerHome = tool 'SonarQubeScanner'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
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
