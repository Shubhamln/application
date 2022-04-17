pipeline{
  agent any
  environment{
    PATH = "usr/share/bin:$PATH"
  }
  stages{
    stage("Git checkout"){
	  steps{
	    git branch: 'main', credentialsId: 'Github', url: 'https://github.com/Shubhamln/application.git'
	  }
	}
	stage("Maven Build"){
	  steps{
	    sh "mvn clean package"
		sh "mv target/*.war target/myapp.war"
	  }
	}
	stage("Deploy"){
	  sshagent(['SSH']) {
        sh """
		  scp ssh -o StrictHostKeyChecking=no target/myapp.war ec2-user@172.31.84.32:/opt/bin/tomcat/webapps/
		  shh /usr/bin tomcatdown
		  shh /usr/bin tomcatup
		"""
      }  
	}
  }
}
