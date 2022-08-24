pipeline {
   agent { label 'docker' }
   stages {
	stage('Tooling version') {
	   steps {
	      sh "docker --version" 
	      sh "docker-compose version"
	   }
      } 
	stage('Checkout') {
            steps{
                git branch: 'main',
                    url: 'https://github.com/denyskods/docker-issue.git'        
                }
            }
	stage('docker-compose build') {
           steps {
             script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub_cred_denisko', passwordVariable: 'HUB_KEY', usernameVariable: 'HUB_USR')]) {
              sh ''' 
	      docker-compose stop
         docker-compose down
         docker pull hello-world
	      docker system prune -f
	      docker image rm -f $(docker image ls -q)
	      docker-compose build
	      docker login -u "$HUB_USR" -p "$HUB_KEY"
	      docker-compose push
	      '''
           }
       }
     }
  }	
        stage('docker-compose deploy') {
           steps {
              sh "docker-compose up -d"
           }
       }
        stage('docker-compose status') {
           steps {
              sh "docker-compose ps"
           }
       }
        stage('docker-push') {
           steps {
              sh  '''
           docker-compose ps
	      '''	
           }
       }
        stage('telegram push') {
           steps {
         
           telegramSend(message: 'Hello World', chatId: -601935342)
	      	
           }
       }


   }
}
