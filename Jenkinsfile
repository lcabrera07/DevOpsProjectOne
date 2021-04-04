pipeline {
  environment {
    registry = "lcabrera07/devops_course_projects"
  }
  
  agent any
    
  tools {nodejs "NodeJS"}
    
  stages {
        
    stage('Git') {
      steps {
        git ([url: 'https://github.com/lcabrera07/DevOpsProjectOne.git', branch: 'main', credentialsId: 'GitHubSSH'])
      }
    }
     
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
    
    stage('Building Docker Image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry('', 'DockerHubCredentials') {
            dockerImage.push("$BUILD_NUMBER")
            dockerImage.push('latest')
          }
        }
      }
    }
    
  }
}
