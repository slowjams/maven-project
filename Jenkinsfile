pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}