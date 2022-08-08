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
                sh 'docker build .'
            }
        }
        stage('Docker Login'){
            
            steps {
                       withCredentials([usernameColonPassword(credentialsId: 'Docker', variable: 'Dockerpwd')]){
                       sh "docker login -u mrmeowboi -p ${Nandhaat25}"
                   }
            }                
        }
        stage('Docker Push'){
            steps {
                sh 'docker push mrmeowboi/docker_jenkins_springboot:${BUILD_NUMBER}'
            }
        }
        stage('Docker deploy'){
            steps {
               
                sh 'docker run -itd -p  8081:8080 mrmeowboi/docker_jenkins_springboot:${BUILD_NUMBER}'
            }
        }
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
