pipeline {
    agent any
    tools {
        maven 'localMaven'
    }

    triggers{
        pollSCM('* * * * *')
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

        stage('Deploy to staging and prod'){
 
        parallel{
            stage('Deploy to stage'){
              steps{
              bat "cp **/target/*.war /c/Users/ak15023/Downloads/apache-tomcat-8.5.50/webapps/"
            }

            stage('Deploy to prod'){
              steps{
               bat "cp **/target/*.war /c/Users/ak15023/Downloads/apache-tomcat-8.5.50-prod/webapps/"
            }

        }
    }
}

}