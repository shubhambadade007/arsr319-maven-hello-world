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
    }
}
