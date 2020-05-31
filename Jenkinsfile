pipeline {
        agent any
        stages{
            stage('Build'){
                steps{
                sh 'mvn clean package'

                }
                post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/**/*.war'
                }
            }
            }
            stage('Bake Image'){
                steps{
                sh "/usr/bin/packer build -var 'component=backend-${BUILD_NUMBER}' packer.json"

                }
            }
            

        }

}

