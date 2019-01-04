
pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('DeployToStage'){
            steps {
                    build job: 'DeployArtifactStagingTomcat'
            }
        }
        stage('DeployToProd'){
            steps {
                timeout(time:5, unit:'DAYS'){
                input message: 'Approve for deployment'
                }
              build job: 'DeployArtifactProdTomcat'
            }
            post {
                success{
                    echo "its passed"
                }
                failure{
                    
                    echo "FAILED"
            }
        }       
    }
}
