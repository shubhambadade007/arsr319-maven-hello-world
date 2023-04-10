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
         stage("build dockerimage"){
            steps{
                script{
               docker.build('shubhamimage', '.')
                }
           }
        }
        stage('run image '){
            steps{
                script{
                    // This step should not normally be used in your script. Consult the inline help for details.
                    withDockerContainer('shubhamimage') {
                    // some block
                   }
                }
            }
            
        }
         stage("rum one more image from shebhimage"){
            steps{
                sh 'docker run -d --name shubhambadade07/java_app shubhamimage /bin/bash'
            }
        }
        stage("rum one more image from shebhimage"){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubpass', usernameVariable: 'dockerhubuser')]) {
                        sh 'docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}'
                        sh 'docker push shubhambadade07/java_app:latest'
    // some block
                   }
               }
            }
        }
    }
}
