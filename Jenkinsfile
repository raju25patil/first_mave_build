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
        stage('Deploying to Production'){
          steps {
            timeout(time:5, unit:'DAYS'){
            input message: 'Approve Prodction Deployment ? '
            }

            build job: 'deploy-to-production'

          }
          post {
              success{
                echo 'Prod deployment complted'
              }
              failure{
                echo 'Prod deployment failed'
              }

          }
        }
    }
}
