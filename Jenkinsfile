pipeline {
    agent any
    tools {
        maven 'localMaven'
    }
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy to staging'){
            steps {
                build job: 'deploy-to-staging'
            }
        }

        stage('Deploy to Prod'){
            steps{

                timeout(time: 2, unit: 'DAYS') {
                    input message: 'Approve Deploy?'
                }
                build job: 'deploy-to-prod'
            }

            post {
                success {
                    echo 'Production deployment successful'
                }

                failure {
                    echo 'Production deployment failed'
                }
            }
        }
    }
}
