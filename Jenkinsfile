pipeline {

   agent any

   stages {
	stage('Tooling version') {
	   steps {
	      sh "docker --version" 
	      sh "docker-compose version"
	   }
      } 	
	stage('docker-compose build') {
           steps {
              sh ''' 
              docker pull hello-world
	      docker system prune -f
	      docker image rm -f $(docker image ls -q)
	      docker-compose build
	      '''
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

   }
//   post {
//      always {
//        sh "docker-compose down || true"
//      }
//   }   
}
