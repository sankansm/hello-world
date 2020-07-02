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
                sh "/usr/local/bin/packer build -var 'job=${JOB_NAME}' -var 'build_number=${BUILD_NUMBER}' -var 'component=${JOB_NAME}-${BUILD_NUMBER}' packer.json"

                }
            }
            stage('Deploy'){
                steps{
                    input message: "Approve the Deploy?"
                    sh '/usr/local/bin/terraform init'

                    sh '/usr/local/bin/terraform apply -var component=${JOB_NAME}-${BUILD_NUMBER} -auto-approve'
                }
            }




        }

}
