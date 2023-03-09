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
               when {
                branch "master"
           }

    	   }
 	}

	stage('3-Deploy') {
           steps {
               echo  "Start of Stage Deploy"
               sh '''
                hostname
                '''

    	   }
	}

    }
}
