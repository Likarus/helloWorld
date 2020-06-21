pipeline {
environment {
registry = "rafaelhd/trancerepo"
registryCredential = 'rafaelhd'
dockerImage = ''
}	
	agent any
	stages{
		stage ("Clean"){
			steps{
				bat "mvn clean"
			  }
			}
		
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                        bat 'mvn sonar:sonar'
                    }
              	  }
       		 }	
		
		stage ("package"){
			steps{
				bat "mvn package"
				archiveArtifacts "dist/*.war"
			  }
			}
		
		stage('Build image') {
            steps {
                echo 'Starting to build docker image'

                script {
                    def customImage = docker.build("rafaelhd/trance_repo:${BUILD_NUMBER}")
                
              		 }
           	    }
        	}
	stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
	
	}
	
}
