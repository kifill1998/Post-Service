pipeline {
    agent any

    stages {        
         stage('Test A') {
            when  { anyOf {
                branch 'master/*'
            }
        }
            steps {
                dir('src/') {
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
