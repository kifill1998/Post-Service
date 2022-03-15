pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    stages {
        stage('Build') {
            steps {
                sh './gradlew clean check --no daemon'
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
