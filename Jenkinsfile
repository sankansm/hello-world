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
				archiveArtifacts artifacts: '**/*.war'
				}
			}
		}
		
	
		}

}
