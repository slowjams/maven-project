pipeline {
    agent any
    tools {
        maven 'local maven'
    }
    
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to staging'){
            steps {
                build job:'deploy-to-staging'
            }
        }
        stage('Deploy to Production'){
            steps {
                timeout(time:5, unit:'DAYS') {
                    input message: 'Do you want to deploy it to Production?'
                }
            }
            post {
                success {
                    echo 'Successfully deployed to Production'
                }

                failure {
                    echo 'Failed to deployed to Production'
                }
            }
        }
    }
}