pipeline {
    agent any

    stages {
         stage('build') {
            steps {
                sh 'docker build -t hemaecr .'
            }
        }
        stage('push') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 516615020300.dkr.ecr.us-east-1.amazonaws.com'
                sh 'docker tag hemaecr:latest 516615020300.dkr.ecr.us-east-1.amazonaws.com/hemaecr:latest'
                sh 'docker push 516615020300.dkr.ecr.us-east-1.amazonaws.com/hemaecr:latest'
            }
        }
        stage('deploy'){
            steps{
                sh 'docker run -d --name nodejs-app -p 8080:8081 516615020300.dkr.ecr.us-east-1.amazonaws.com/hemaecr:latest'
            }
        }

    }
}
