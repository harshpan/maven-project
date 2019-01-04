
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
    }
}
