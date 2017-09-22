node {
	echo 'Microservice CI/CD Pipeline - Eureka Server' 
	
    properties([pipelineTriggers([githubPush()])])
	
	stage ('Pull Repository') {
		checkout scm
	}
}