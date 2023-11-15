pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {sh 'mvn clean verify sonar:sonar 
                       -Dsonar.projectKey=learningdevsecops 
                       -Dsonar.organization=learningdevsecops 
                       -Dsonar.host.url=https://sonarcloud.io 
                       -Dsonar.login=d527f5658b596c43fdcd8cfdf2b9a9104eba34c7'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				            withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}