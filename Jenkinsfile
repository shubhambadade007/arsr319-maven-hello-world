pipeline {
    agent any
    stages{
        stage("checkout from scm"){
            steps{
                script{
                    git 'https://github.com/shubhambadade007/arsr319-maven-hello-world.git'
                }
            }

        }
        
         stage("mvn build "){
            steps{
                sh 'mvn clean package'
            }
        } 
        stage("code analysis"){
            steps{
                script{
                 
                  withSonarQubeEnv(credentialsId: 'sonar_token') {
                 sh 'mvn clean package sonar:sonar'
                  }
    
                }
            
            }
        }
        /*
        
         stage("build dockerimage"){
            steps{
                script{
               docker.build('shubhamimage', '.')
                }
           }
        }
        */
        stage('run image '){
            steps{
                sh 'docker build -t shubhambadade07/java_app:latest .'
            }
            
        }
        
         
        stage("push image "){
            steps{
                script{
                
                    withCredentials([usernamePassword(credentialsId: 'dockerhub_new', passwordVariable: 'dockerhubpass', usernameVariable: 'shubhambadade')] {
                        sh 'docker login -u ${env.shubhambadade} -p ${env.dockerhubpass} docker.io'
                        sh 'docker push shubhambadade07/java_app:latest'
    
                    }
               }
            }
        }
        
    }
}
