pipeline{
  agent any
  stages{
    stage('build'){
      steps{
        sh 'docker-compose down && docker-compose up -d --build'
      }
    }
    stage('test frontend'){
      steps{
        sh 'cd frontend && python3 -m pytest' 
      }
    }
    stage('test backend'){
      steps{
	sh 'cd backend && python3 -m pytest'
      }
    }   
    stage('deploy')
      steps{
	sh 'docker stack deploy docker-compose.yaml'
      }
    }
  }
}
