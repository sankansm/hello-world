pipeline {
	agent any
	
	stages{
		stage('Build'){
		
			steps{
			sh 'mvn clean package'
			}
			post{
				success{
				echo "now Archiving the artefact"
				archiveArtefacts artefacts: '**/*.war'
				}
			}
		}
		
		stage('Deploy to stage'){
		
			steps{
				build job: 'deploy_to_staging'
		
		}
		
		}
		
		stage('Deploy to prod'){
		
				steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }

                build job: 'Deploy-to-Prod'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
	
							}
		
	
		}

}
