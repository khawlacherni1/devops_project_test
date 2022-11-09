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
    }
}