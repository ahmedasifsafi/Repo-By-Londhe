pipeline {
    agent any

    stages {
        stage('Cloning') {
            steps {
                echo 'Code Cloning'
                git url: "https://github.com/ahmedasifsafi/my-new-repo.git", branch: "main"
             }
                 }
        stage('Build') {
            steps {
                echo 'Code Building'
                sh "docker build -t myapp ."
                }
            }
        stage('Deploy') {
            steps {
                echo 'Code Deployment to Docker HUB'
                withCredentials([usernamePassword(credentialsId:"DockerHubUserPass", passwordVariable:"HubPass", usernameVariable: "HubUser" )]){
                sh "docker tag myapp ${HubUser}/myapp:latest"
                sh "docker login -u ${HubUser} -p ${HubPass} "            
                sh "docker push ${HubUser}/myapp:latest"    
                 }
                }
              }     
        stage('Container Creation') {
            steps {
                echo 'Creating Container'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
