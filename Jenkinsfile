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
}
