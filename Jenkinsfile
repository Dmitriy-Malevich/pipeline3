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
               sh  "hostname | grep 4Jenkins-Slave"
               echo  "End of Stage Build"
    	   }
 	}

	stage('3-deploy') {
           steps {
               echo  "Start of Stage Build"
               sh "pwd"
               echo  "Building.............."
               echo  "End of Stage Build"
    	   }
	}

    }
}
