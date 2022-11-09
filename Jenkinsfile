pipeline {
    agent any

    tools {
            maven 'MAVEN_HOME'

        }

    stages{
        stage('Checkout') {
                        steps{
                             script{
                                   git "https://github.com/khawlacherni1/devops_project_test.git"
                                   }
                             }
                    }

        stage('Maven-clean'){
                        steps{
                             script{
                                    sh 'mvn clean'
                                        }
                                    }
                                }

         stage('MVN COMPILE'){
                     steps{
                         sh  'mvn compile'
                     }
                 }

                 stage('MVN PACKAGE'){
                       steps{
                           sh  'mvn package'
                       }
                 }

         stage('MVN SONARQUBE'){

                         steps{
                                   sh  'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=99818823'
                         }
                   }

                   stage('Email Notification'){
                               steps{
                                   script{
                                       mail bcc: '', body: '''Hi,
                   Welcome to jenkins email alerts.
                   Thanks,
                   khawla''', cc: '', from: '', replyTo: '', subject: 'Jenkins Job', to: 'khawla040200@gmail.com'
                                   }
                               }
                           }

    }
}