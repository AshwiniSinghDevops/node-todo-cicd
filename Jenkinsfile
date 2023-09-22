pipeline {
    agent {label 'dev-agent'}
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/AshwiniSinghDevops/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t ashwinisingh007/node-todo-app-cicd:latest"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ashwinisingh007/node-todo-app-cicd:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
