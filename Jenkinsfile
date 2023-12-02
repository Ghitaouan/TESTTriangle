pipeline{
	agent any
	tools{
    	maven 'AjoutMaven'
	}
	stages{
    	stage('git checkout'){
        	steps{
            	git 'https://github.com/Ghitaouan/TESTTriangle.git'
        	}
    	}
    	stage('Build the application'){
        	steps{
            	sh 'mvn clean install'
        	}
    	}
    	stage('Unit Test Execution'){
        	steps{
            	sh 'mvn test'
        	}
    	}
    	stage('Build the docker image'){
        	steps{
            	sh 'docker build -t ghitadevops/wallneryan .'
        	}
    	}
    	stage('push the dokcker image'){
        	steps{
            	withCredentials([usernamePassword(credentialsId: 'dockerhubpass',usernameVariable:'dockerHubUser', passwordVariable: 'dockerHubPass')]){
                	sh "docker login -u ghitadevops -p ouannaneghita"
            	}
                	sh "docker push ghitadevops/wallneryan:latest"
        	}
    	}
	}
  post {
        failure {
                emailext body: "Le Build a échoué.",
                          to: 'g.ouannane@gmail.com',
                          recipientProviders: [requestor()],
			  subject: "Build"
        }
    }
}
