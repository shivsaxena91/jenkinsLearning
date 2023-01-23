pipeline{
	agent any
	
	environment{
		NEW_VERSION = '1.3.0'
		//SERVER_CREDENTIALS = credentials("server-credentials")
	}
	
	tools{
		maven 'Maven'
	}
	
	parameters{
		choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description:'')
		booleanParam(name: 'executeTests', defaultValue: true, description:'')
	}
	
	stages{
		stage('Build'){
			steps{
				echo 'Building the application....'
				echo "Building version ${NEW_VERSION}"
				sh "mvn install"
			}
		}
		
		stage('Test'){
			when{
				expression{
					BRANCH_NAME='master'
					params.executeTests == true
				}
			}
			steps{
				echo 'Testing the application....'
			}
		}
		
		stage('Deploy'){
			steps{
				echo 'Deploying the application....'
				echo "Deploying version ${params.VERSION}"
				//echo "Deploying with ${SERVER_CREDENTIALS}"
				//sh "${SERVER_CREDENTIALS}"
				//withCredentials([
				//	usernamePassword:(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)]){
				//		sh "some script ${USER} ${PWD}"
				//}
			}
		}
	}
}
