pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh '/Users/Shared/apache-maven-3.5.4/bin/mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploying to staging'){
          steps {
            build job: 'deploy-to-staging'
          }
        }
    }
}
