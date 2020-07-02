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
                sh "/usr/bin/packer build -var 'build_number=${BUILD_NUMBER}' -var 'component=${JOB_NAME}-${BUILD_NUMBER}' packer.json"

                }
            }
            stage('Deploy'){
                steps{
                    input message: "Approve the Deploy?"
                    sh 'terraform init'

                    sh 'terraform apply -var component=${JOB_NAME}-${BUILD_NUMBER} -auto-approve'
                }
            }




        }

}
