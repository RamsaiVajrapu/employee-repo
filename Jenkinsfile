pipeline {
  agent any
  stages {	
	stage('Maven Compile'){
		steps{
			echo 'Project compile stage'
			bat label: 'Compilation running', script: '''mvn compile'''
	       	}
	}
	
	stage('Unit Test') {
	   steps {
			echo 'Project Testing stage'
			bat label: 'Test running', script: '''mvn test'''
	       
       }
   	}
	
	/*
	stage('Publish Test Coverage Report') {
         steps {
           step([$class: 'JacocoPublisher', 
                execPattern: '**/build/jacoco/*.exec',
                classPattern: '**/build/classes',
                sourcePattern: 'src/main/java',
                exclusionPattern: 'src/test*'
                ])
            }
        }
        */
        
    stage('Jacoco Coverage Report') {
        steps{
            jacoco()
		}
	}
        
	stage('SonarQube'){
         steps{
            bat label: '', script: '''mvn sonar:sonar \
		 -Dsonar.host.url=http://localhost:9000 \
 		-Dsonar.login=c6bd39972c9e29699faceb08bb2c876d08fed9cd'''
          }
	
	stage('Maven Package'){
		steps{
			echo 'Project packaging stage'
			bat label: 'Project packaging', script: '''mvn package'''
		}
	} 		
    
  }
}