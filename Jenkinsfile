node {
  stage 'Checkout'
  git url: 'https://github.com/prostraciya/docker-issue.git'

  stage 'build'
  docker-compose build

  stage 'deploy'
  docker-compose up
}
