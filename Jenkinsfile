pipeline {
 environment {
        registry = 'kifill1998/kevinifill'
        dockerHubCreds = 'docker_hub'
        dockerImage = ''
    }
 agent any
    stages {
//      node {
//   stage('SCM') {
//     checkout scm
//   }
//   stage('SonarQube Analysis') {
//     def mvn = tool 'Default Maven';
//     withSonarQubeEnv() {
//       sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=sadfsdf"
//     }
//   }

//      stage('SonarCloud') {
//   environment {
//     SCANNER_HOME = tool 'SonarQubeScanner'
//     ORGANIZATION = "igorstojanovski-github"
//     PROJECT_NAME = "igorstojanovski_jenkins-pipeline-as-code"
//   }
//   steps {
//     withSonarQubeEnv('SonarCloudOne') {
//         sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
//         -Dsonar.java.binaries=build/classes/java/ \
//         -Dsonar.projectKey=$PROJECT_NAME \
//         -Dsonar.sources=.'''
//     }
//   }
// }
        stage('Test') {
            when {
                branch 'master/*'
            }
        steps {
            withMaven {
                cleanWs()
                sh 'test'
            }
         }
       }
       stage('Build') {
          when {
             branch 'master'
          }
          steps {
            withMaven {

              sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=kifill1998_Post-Service'
              //sh 'mvn -f Post-Service/pom.xml clean package -DskipTests'

            }
          }
       }
       stage('Docker Build') {
           when {
               branch 'master'
           }
           steps {
            dir('Post-Service') {
               script {
                  echo "$registry:$currentBuild.number"
                  dockerImage = docker.build "$registry"
               }
            }
           }
       }

       stage('Docker Deliver') {
           when {
               branch 'master'
           }
           steps {
               script {
                   docker.withRegistry('', dockerHubCreds) {
                       dockerImage.push("$currentBuild.number")
                       dockerImage.push("latest")
                   }
               }
           }
        }
      
stage('Wait for approval') {
        when {
            branch 'master'
        }
        steps {
            script {
                try {
                    timeout(time: 1, unit: 'MINUTES') {
                        approved = input message: 'Deploy to production?', ok: 'Continue',
                            parameters: [choice(name: 'approved', choices: 'Yes\nNo', description: 'Deploy build to production')]
                        if(approved != 'Yes') {
                            error('Build did not pass approval')
                        }
                    }
                } catch(error) {
                    error('Build failed because timeout was exceeded')
                }
            }
        }
    }
//  stage('Deploy to GKE') {
//                 when {
//                     branch 'master'
//                 }
//                 steps{
//                     sh 'sed -i "s/%TAG%/$BUILD_NUMBER/g" ./Post-Service/k8s/deployment.yml'
//                     sh 'cat ./Post-Service/k8s/deployment.yml'
//                     step([$class: 'KubernetesEngineBuilder',
//                         projectId: 'revbanking',
//                         clusterName: 'revbanking-gke',
//                         zone: 'us-central1',
//                         manifestPattern: 'Post-Service/k8s/',
//                         credentialsId: 'revbanking',
//                         verifyDeployments: true
//                     ])
//                                }
//                             }
    } 
}
