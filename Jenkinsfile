node {
	echo ' Microservice CI/CD Pipeline - Eureka Server ' 
	echo "#################### Initiating ${env.BRANCH_NAME} Build ####################"
    def commit
    		
    properties([pipelineTriggers([githubPush()])])
    
	docker.image('maven:3.3.3-jdk-8').inside {
	stage ('Pull Repository') {
		checkout scm
		gitCommit = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
        commit = gitCommit.take(6)
		echo 'commit value: #{commit}'
	}
	
	stage('Build Java') {
	    sh "mvn dependency:purge-local-repository"
		sh "mvn clean install"
      	sh 'cp ./target/eureka-server-0.0.1-SNAPSHOT.jar ./eureka-server-0.0.1-SNAPSHOT.jar'
	}
  }
  
   stage ('Build Docker Images') {
    docker.withRegistry('https://index.docker.io/v1/','docker-hub-credentials') {
      def app = docker.build("madhankumardocker/eureka-server:${commit}")
    }
  }
  
    stage ('Push Docker tags') {
      docker.withRegistry('https://index.docker.io/v1/','docker-hub-credentials') {
        app = docker.image("madhankumardocker/eureka-server:${commit}")
        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
      }
  }
}
