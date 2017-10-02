node {
	echo ' Microservice CI/CD Pipeline - Eureka Server ' 
	echo "#################### Initiating ${env.BRANCH_NAME} Build ####################"
		
    properties([pipelineTriggers([githubPush()])])
	docker.image('maven:3.3.3-jdk-8').inside {
	stage ('Pull Repository') {
		checkout scm
	}
	
	stage('Build Java') {
	    sh "mvn dependency:purge-local-repository"
		sh "mvn clean install"
      	sh 'cp ./target/apollo-accounting-revrec-services-1.0.0-SNAPSHOT.jar ./apollo-accounting-revrec-services-1.0.0-SNAPSHOT.jar'
	}
  }
}
