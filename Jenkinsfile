pipeline {
    agent any
    environment {
                               DOCKERHUB_CREDENTIALS = credentials('dockerhubtocken')
                               DOCKERHUB_CREDENTIALS_USR = "khawlachrerni"
                               DOCKERHUB_CREDENTIALS_PSW  = "99818823khawla"
                               EMAIL_TO = 'khawla.cherni@esprit.tn'
                           }

    tools {
            maven 'MAVEN_HOME'

        }
    post {
                    failure {
                        emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}',
                                to: "${EMAIL_TO}",
                                subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
                    }
                    unstable {
                        emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}',
                                to: "${EMAIL_TO}",
                                subject: 'Unstable build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
                    }
                    changed {
                        emailext body: 'Check console output at $BUILD_URL to view the results.',
                                to: "${EMAIL_TO}",
                                subject: 'Jenkins build is back to normal: $PROJECT_NAME - #$BUILD_NUMBER'
                    }
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


        /*stage ('Publish to Nexus') {
                            steps{
                                 script{
                                 nexusPublisher nexusInstanceId: 'INSTANCE_IN_JENKINS_SETTINGS', nexusRepositoryId: 'pipeline', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: './target/gift-shop-api.war']],mavenCoordinate: [artifactId: 'gift-shop-mono', groupId: 'com.online', packaging: 'war', version: '1']]]
                                    }
                                    }
                        }*/

                   /*stage('Email Notification'){
                               steps{
                                   script{
                                       mail bcc: '', body: '''Hi,
                   Welcome to jenkins email alerts.
                   Thanks,
                   khawla''', cc: '', from: '', replyTo: '', subject: 'Jenkins Job', to: 'khawla040200@gmail.com'
                                   }
                               }
                           }*/



                   stage('push docker hub') {
                               steps {
                                   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'
                                    sh 'docker push docker.io/khawlacherni/khawlapidevtest'

                               }
                           }

    }
}