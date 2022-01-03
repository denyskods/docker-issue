node {
  stage 'Checkout'
  git url: 'https://github.com/prostraciya/docker-issue.git'

  stage 'build'
 sh '''
 docker-compose build
'''

 stage 'deploy'
 sh '''
 docker-compose up
 '''












  stage 'deploy'
  docker-compose up
}
