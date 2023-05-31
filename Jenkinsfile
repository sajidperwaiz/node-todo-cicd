pipeline {
    agent { label 'node-agent'}
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/sajidperwaiz/node-todo-cicd.git', branch: 'master'
            }
            
        }
        stage('Build'){
            steps{
                sh 'docker build . -t sajidperwaiz/node-todo-test:latest'
            }
            
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable: 'dockerHubPassword',usernameVariable:'dockerHubUser')]){
                 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push sajidperwaiz/node-todo-test:latest'
                }
            }
            
        }
        stage('Test'){
            steps{
                echo "Test the new build.."
            }
            
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
