properties([pipelineTriggers([githubPush()])])
pipeline {
    agent {
	label 'ubuntu_slave'
}

    stages {
        stage('1-Build') {
           steps {
               echo  "Start of Stage Build"
 	       sh "pwd"
               echo  "Building..............."
               echo  "End of Stage Build"
   	   }
	}
	stage('2-Test') {
           steps {
               echo  "Start of Stage Test"
               sh "cat index.html | grep Вторая"
               sh  "hostname | grep Jenkins-Slave"
               echo  "End of Stage Build"
    	   }
 	}

	stage('3-Deploy') {
           steps {
               echo  "Start of Stage Deploy"
               sh "rm /var/www/html/index.nginx-debian.html"
	       sh "mv /root/jenkins/workspace/ker_multibranch_pipeline3_master/index.html /var/www/html/
	       sh "systemctl restart nginx"
               echo  "Building.............."
               echo  "End of Stage Deploy"
    	   }
	}

    }
}
