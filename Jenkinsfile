pipeline {
    agent any 
    stages {
        stage('Compile and Clean') { 
            
            steps {
                sh "mvn clean compile"
            }
        }
        stage('deploy') { 
            
            steps {
                sh "mvn package"
            }
        }
        stage('Build Docker image'){
          
            steps {
                echo "Hello Java Express"
                sh 'ls'
                sh 'sudo docker build -t  docker_jenkins_springboot:${BUILD_NUMBER} .'
            }
        }
        stage('Docker Login'){
            
            steps {
                       withCredentials([usernameColonPassword(credentialsId: 'Docker', variable: 'Dockerpwd')]){
                       sh "sudo docker login -u mrmeowboi -p ${Nandhaat25}"
                   }
            }                
        }
        stage('Docker Push'){
            steps {
                sh 'sudo docker push mrmeowboi/docker_jenkins_springboot:${BUILD_NUMBER}'
            }
        }
        stage('Docker deploy'){
            steps {
               
                sh 'sudo docker run -itd -p  8081:8080 mrmeowboi/docker_jenkins_springboot:${BUILD_NUMBER}'
            }
        }
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
