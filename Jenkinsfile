pipeline{
    agent any
    stages{
            stage('BUILD'){
                steps{
                    bat 'mvn clean package'
                    bat "docker build . -t tomcatwebapp:${env.BUILD_ID}"
             }

         }
    }

}