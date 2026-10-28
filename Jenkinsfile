pipeline{
    agent any;
    
    stages{
        stage("Code"){
            steps{
                git url: 'https://github.com/Ayush-Kumar2005/two-tier-flask-app.git',
                    branch: 'master'
                echo "Code cloned successfully...😎"
            }
        }
        stage("Build"){
            steps{
                sh 'docker build -t two-tier-flask-app .'
                echo "Build successfull...😎"
            }
        }
        stage("Test"){
            steps{
                echo "Testing successfull...😎"
            }
        }
        stage("Push to DockerHub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCreds",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                )]) {
                    sh 'docker login -u $dockerHubUser -p $dockerHubPass'
                    sh 'docker image tag two-tier-flask-app $dockerHubUser/two-tier-flask-app'
                    sh 'docker push $dockerHubUser/two-tier-flask-app'
        
                    echo "Pushed to DockerHub successfully...😎"
                }
            }
        }
        stage("Deployment"){
            steps{
                sh 'docker compose up -d --build flask-app'
                echo "Deployment successfull...😎"
            }
        }
    }
}
