pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    stages {
        stage('Build') {
            steps {
                sh './mvnw clean check -v'
            }
        }
//         stage('Trial') {
//             steps {
//                  withMaven {
//                     mvn clean
//                 }
//             }
//         }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post {
        always {
            junit(
                allowEmptyResults: true, 
                testResults: '**/build/test-results/test/*.xml'
            )
            recordIssue(
                enabledForFailure: true, aggregatingResults: true,
                tools: [java(), checkStyle(pattern: '**/build/**/main.xml', reportEncoding: 'UTF-8)]
        }
    }
}
