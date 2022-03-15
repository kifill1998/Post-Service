pipeline {
    agent any

    stages {        
        stage('Testing') {          
             steps {
                  withMaven {
                     sh 'mvn test'
                 }
             }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
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
}
