pipeline{
  agent any
  stages{
    stage("Git checkout"){
	  steps{
	    git branch: 'main', credentialsId: 'Github', url: 'https://github.com/Shubhamln/application.git'
	  }
    }
    stage("Maven package"){
      steps{
        sh "mvn clean package"
	   }
    }

  }
}
