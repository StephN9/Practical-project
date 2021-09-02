pipeline{
  agent any
  stages{
    stage('install docker'){
      steps{
        sh 'sudo apt update && curl https:get.docker.com | sudo bash'
      }
    }
    stage('install docker-compose'){
      steps{
        sh 'sudo apt install jq && version=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r '.tag_name') && sudo curl -L "https://github.com/docker/compose/releases/download/${version}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose'
      }
    }
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
  }
}
