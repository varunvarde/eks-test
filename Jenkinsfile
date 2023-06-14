pipeline {
    agent any 
    stages {
        stage('configureing kubectl') {    
            steps {
                sh 'cat ${HOME}/.kube/config'
            }
        }
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
               sh 'kubectl apply -f deploy.yml && kubectl get svc'
            }
        }
        stage ('verifying deployment') {
            steps {
            sh 'kubectl get deploy test-springboot'
            }
        }
    }
}
