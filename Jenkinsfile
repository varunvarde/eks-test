pipeline{
    agent any
    
    stages{
        

    stage("Git Clone"){
        steps{

        git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/nadeem9975/eks-test.git'
            }

            }
    stage('docker build image'){
        steps{
        sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID . '
        sh 'docker image tag $JOB_NAME:v1.$BUILD_ID nadeem9975/$JOB_NAME:v1.$BUILD_ID'
        sh 'docker image tag $JOB_NAME:v1.$BUILD_ID nadeem9975/$JOB_NAME:latest'
    }
    }
    stage('pushing images to dockerHub'){
      steps{
          
        withCredentials([string(credentialsId: 'nadeem9975', variable: 'DOCKER_HUB_PASSWORD')]) 
        sh 'docker login -u nadeem9975 -p Nadeem@1995'
        sh 'docker image push nadeem9975/$JOB_NAME:v1.$BUILD_ID'
        sh 'docker image push nadeem9975/$JOB_NAME:latest'
        sh 'docker image rm $JOB_NAME:v1.$BUILD_ID nadeem9975/$JOB_NAME:v1.$BUILD_ID nadeem9975/$JOB_NAME:latest'
        }
    }
    
    stage("kubernetes deployment"){
        steps{
        sh 'kubectl apply -f deploy.yml'
    }
   } 
 }
}
