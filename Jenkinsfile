pipeleline{
    agent any

    stages{

        stage('Fetch'){
            steps{
                git url: 'https://github.com/akhilvijay15/todays_jenkins.git' , branch : 'main'
            }
        }

        stage('Build'){
             steps{
                sh 'docker build . -t akhilvijay15/dishaapp:latest'
             }
        }

        stage('DockerPush'){
              steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubPassword')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh 'docker push akhilvijay15/dishaapp:latest' 
                }
              }
        }

        stage('Deploy'){
             steps{
                sh "docker-compose down && docker-compose up -d"
             }
        }
    }
}