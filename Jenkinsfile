pipeline{
  agent any
  stages{
    stage('build'){
      steps{
        withCredentials([file(credentialsId: 'DOCKER_COMPOSE', variable: 'DOCKER_COMPOSE')]) {
          sh 'cp "$DOCKER_COMPOSE" ./docker-compose.yaml'
          sh 'docker-compose build'
          sh 'rm docker-compose.yaml'
        }
      }
    }
    stage('test frontend'){
      steps{
        sh 'cd frontend && python3 -m pytest > frontendtest.txt'
      }
      post {
        always {
            archiveArtifacts artifacts: 'frontend/frontendtest.txt', onlyIfSuccessful: true
        }
      }
    }
    stage('test backend'){
      steps{
        sh 'cd backend && python3 -m pytest > backendtest.txt'
      }
      post {
        always {
            archiveArtifacts artifacts: 'backend/backendtest.txt', onlyIfSuccessful: true
        }
      }
    }

    stage('deploy'){
      steps{
        withCredentials([file(credentialsId: 'DOCKER_COMPOSE', variable: 'DOCKER_COMPOSE')]) {
          sh 'cp "$DOCKER_COMPOSE" ./docker-compose.yaml'
          sh 'docker stack deploy --compose-file docker-compose.yaml practical-project-stack'
          sh 'rm docker-compose.yaml'
        }
      }
    }
  }
}
