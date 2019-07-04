pipeline {
        agent any
         stages{
                stage('Init'){
                        steps {
                         echo "Nothing to do"
                        }
                }

                stage('Build'){
                        steps {
                         echo "Building..."
			 sh 'mvn clean package'
                        }
			post {
			 success {
			  echo 'Now archiving...'
			  archiveArtifacts artifacts: '**/target/*.war'
				 }
			}
                }

                stage('Deploy to Staging'){
                        steps {
                         echo "Deploying..."
			 timeout(time:5, unit:'DAYS'){
			 	input message:'Approve prod deployement?'
			 }
			 build job: 'deploy-to-stagging'
                        }
			
			post {
			 success {
				echo 'Code deployed to prod'
			 }
			 failure {
				echo 'Deployment failed'
			 }
			
			}
                }
        }
}

