pipeline{
  agent any
  stages{
    stage("Git checkout"){
	  steps{
	    git branch: 'main', credentialsId: 'Github', url: 'https://github.com/Shubhamln/application.git'
	  }
	}
	stage("Maven Build"){
	  steps{
	    sh "mvn clean package"
		sh "mv target/*.jar target/myapp.jar"
	  }
	}
	stage("Deploy"){
	  steps{
	    sshagent(['ROOT']) {
          sh """
		    scp -o StrictHostKeyChecking=no target/myapp.jar ec2-user@172.31.84.32:/opt/apache-tomcat-9.0.35//webapps/
		    ssh ec2-user@172.31.84.32 /usr/bin/ sudo tomcatdown
		    ssh ec2-user@172.31.84.32 /usr/bin/ sudo tomcatup
		  """
        }
      }	  
	}
  }
}
