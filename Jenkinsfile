pipeline {

   agent { label 'docker' }

   stages {
	stage('Tooling version') {
	   steps {
	      sh "docker --version" 
	      sh "docker-compose version"
	   }
      } 	
	stage('docker-compose build') {
           steps {
             script {
                    withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'HUB_KEY', usernameVariable: 'HUB_USR')]) {
              sh ''' 
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


   }
}
