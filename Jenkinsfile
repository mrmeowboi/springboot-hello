pipeline {
    agent any    
    stages {
        stage('Compile and Clean') { 
            steps {
                // Run Maven on a Unix agent.
              
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
                sh 'docker build -t  mrmeowboi/anvbhaskar:${BUILD_NUMBER} .'
            }
        }
        stage('Docker Login'){
            
            steps {
                   withCredentials([usernameColonPassword(credentialsId: 'docker-login', variable: 'Dockerpwd')]){
                       sh "sudo docker login -u mrmeowboi -p ${Dockerpwd}"
                   }
            }                
        }
        stage('Docker Push'){
            steps {
                sh 'sudo docker push mrmeowboi/anvbhaskar:${BUILD_NUMBER}'
            }
        }
        stage('Docker deploy'){
            steps {
               
                sh 'sudo docker run -itd -p  8081:8080 mrmeowboi/anvbhaskar:${BUILD_NUMBER}'
            }
        }
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}

