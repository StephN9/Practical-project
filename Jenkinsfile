pipeline{
  agent any
  stages{
    stage('build'){
      steps{
        sh 'cd frontend && docker build'
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
  }
}
