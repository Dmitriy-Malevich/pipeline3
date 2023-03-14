def sendTelegram(message) {
    def encodedMessage = URLEncoder.encode(message, "UTF-8")
    withCredentials([string(credentialsId: 'telegramToken', variable: 'TOKEN'),
    string(credentialsId: 'telegramChatId', variable: 'CHAT_ID')]) {

        response = httpRequest (consoleLogResponseBody: true,
                contentType: 'APPLICATION_JSON',
                httpMode: 'GET',
                url: "https://api.telegram.org/bot$TOKEN/sendMessage?text=$encodedMessage&chat_id=$CHAT_ID&parse_mode=html&disable_web_page_preview=true",
                validResponseCodes: '200')
        return response
    }
}

properties([pipelineTriggers([githubPush()])])
pipeline {
    agent {
	label 'ubuntu_slave'
}
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
        timestamps()
          }

    stages {
        stage('1-Build') {
           steps {
               echo  "Start of Stage Build"
 	       sh '''
		pwd
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
}
