pipeline {
    agent { label 'asd-agent' }
    
    stages{
        stage('code'){
            steps{
                git url: 'https://github.com/akshay15498/node-todo-cicd.git',branch: 'master'
            }
        }
        stage('build'){
            steps{
                sh 'docker build . -t devopsasd/node-todo-app:latest'
            }
        }
        stage('login and push images'){
            steps{
                echo 'login and push images'
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerhubPassword',usernameVariable:'dockerhubUser')]) {
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                    sh "docker push devopsasd/node-todo-app:latest"
                }
            }
        }
        stage('deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
        
    }
}
