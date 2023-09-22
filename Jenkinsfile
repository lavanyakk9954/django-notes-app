pipeline {
    agent any 
    tools{
        Maven = 'maven'
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/lavanyakk9954/django-notes-app.git", branch: "main"
            }
        }
        stage("This is to build the code"){
            steps{
                sh 'mvn compile'
                echo 'Run Success'
            }
        }
stage("This is to package the code"){
            steps{
                sh 'mvn package'
                echo 'Run Success'
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        
    }
}
