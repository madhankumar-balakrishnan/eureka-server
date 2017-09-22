node {
	echo ' Microservice CI/CD Pipeline - Eureka Server ' 
	echo "#################### Initiating ${BRANCH_NAME} Build ####################"
    properties([pipelineTriggers([githubPush()])])
	stage ('Pull Repository') {
		checkout scm
	}
}