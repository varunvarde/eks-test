pipeline {
    agent any
    
    stages{
        
    stage('docker build image'){
        steps{
        sh 'docker image build -t nadeem9975/php:v1 . && '
    }
    }
    stage('pushing images to dockerHub'){
      steps{
          
        withCredentials([string(credentialsId: 'nadeem9975', variable: 'DOCKER_HUB_PASSWORD')]) 
        sh 'docker login -u nadeem9975 -p Nadeem@1995 && docker push nadeem9975/php:v1'
    }
    
    stage("kubernetes deployment"){
        steps{
        sh 'kubectl apply -f deploy.yml'
    }
   } 
 }
}}
