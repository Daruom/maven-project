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
			 build job: 'deploy-to-staging'
                        }
                }
        }
}

