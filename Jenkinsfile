pipeline {
    agent {
	label 'ubuntu_slave'
}
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
        timestamps()
          }

    stages {
        stage('1--Build') {
           steps {
               echo  "Start of Stage Build"
 	       sh '''
		pwd
		hostname
		ls -la
		'''
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
               sh "rm -rf /var/www/html/index.nginx-debian.html"
	       sh "mv index.html /var/www/html"
	       sh "systemctl restart nginx"
               echo  "Building.............."
               echo  "End of Stage Deploy"
    	   }
	}
     }
    post {
        success {
           withCredentials([string(credentialsId: 'botSecret', variable: 'TOKEN'), string(credentialsId: 'chatId', variable: 'CHAT_ID')]) {
           sh  ("""
           curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode=markdown -d text='*${env.JOB_NAME}* : POC *Branch*: ${env.GIT_BRANCH} *Build* : OK *Published* = YES'
           """)
           }
        }

        aborted {
           withCredentials([string(credentialsId: 'botSecret', variable: 'TOKEN'), string(credentialsId: 'chatId', variable: 'CHAT_ID')]) {
           sh  ("""
           curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode=markdown -d text='*${env.JOB_NAME}* : POC *Branch*: ${env.GIT_BRANCH} *Build* : `Aborted` *Published* = `Aborted`'
           """)
           }

        }
        failure {
           withCredentials([string(credentialsId: 'botSecret', variable: 'TOKEN'), string(credentialsId: 'chatId', variable: 'CHAT_ID')]) {
           sh  ("""
           curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode=markdown -d text='*${env.JOB_NAME}* : POC  *Branch*: ${env.GIT_BRANCH} *Build* : `not OK` *Published* = `no`'
           """)
          
	 } 
       }
    }
}
