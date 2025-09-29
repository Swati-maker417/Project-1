pipeline{
    agent any
    tools{
        jdk 'jdk-11'
        maven 'maven'
        }

    stages{
        stage('git-checkout'){
            steps{
                git branch: 'maingit', url: 'https://github.com/Swati-maker417/Project-1.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('test'){
            steps{
                sh  'mvn test'
            }
        }
        stage('build docker image'){
            steps{
                sh 'docker build -t swati954/myapp .'
            }
        }
        stage('container the image'){
            steps{
                sh 'docker run -it --name mycontainer -p 9000:8080 swati954/myapp'
            }
        }
        stage('login to dockerhub'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                    sh 'docker tag myapp $USERNAME/myapp:latest'
                    sh 'docker push $USERNAME/myapp:latest'
                }
            }            
        stage('push the dockerhub'){
            steps{
                sh 'docker push swati954/myapp'
            }
        }
    }   
}