pipeline {
  agent any
  tools { 
        maven 'maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=ade1 -Dsonar.organization=ade1 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=222f13d1b84ec3806b0b45c04830a428c78e235d'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }	

// building docker image
// stage('Build') { 
//             steps { 
//                withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
//                  script{
//                  app =  docker.build("tech365image")
//                  }
//                }
//             }
//     }

// 	stage('Push') {
//             steps {
//                 script{
			
//                     docker.withRegistry("https://924338258393.dkr.ecr.us-east-1.amazonaws.com", "ecr:us-east-1:aws-credentials") 
// 			{
//                     app.push("latest")
//                     }
//                 }
//             }
//     	}


  }
}
