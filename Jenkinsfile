pipeline {
    agent any 
    stages {
        stage('building Image') {    
            steps {
               sh 'docker build . --no-cache -t nadeem9975/php:v1'
            }
        }
        stage('pushing image to hub') { 
            steps {
               sh ' docker  login --username  nadeem9975 --password "Nadeem@1995" && docker push nadeem9975/php:v1 ' 
            }
        }
        stage('Deploying changes') { 
            steps {
               sh 'kubectl apply -f deploy.yml'
            }
        }
    }
}
