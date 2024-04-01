pipeline {
    agent any
    parameters{
        string(name:'tomcat_dev', defaultValue: '35.170.202.149', description: 'Dev Server') 
    //  string(name:'tomcat_prod', defaultValue: 'xxxxxx', description: 'Prod Server') 
    }
    tools {
        maven 'local maven'
    }
    triggers {
        pollSCM('* * * * *')
    }
    
    stages {
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

        stage ('Developments') {
            parallel {
                stage ('Deploy to Dev') {
                    steps {
                        bat "winscp -i C:/tomcat.pem **/target/*.war ec2-user@${params.tomcat_dev}:/opt/apache-tomcat-8.0.23/webapps" 
                        //bat "scp -i C:/tomcat.pem **/target/*.war ec2-user@${params.tomcat_dev}:/opt/apache-tomcat-8.0.23/webapps"              
                    }
                }
                /*
                stage ('Deploy to Prod') {
                    steps {
                        sh "scp -i ..."
                    }
                }
                */
            }
        }
    } 
}