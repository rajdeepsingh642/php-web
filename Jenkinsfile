pipeline {
    agent any
  
   stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/rajdeepsingh642/php-web.git'
            }
        }
       
           stage('build docker image and tag') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker-hub') {
                    sh "docker build -t rajdeepsingh642/php-app:latest ."
                    
                       }
                }
             
            }
        }
            stage('Docker image scan') {
            steps {
             sh "trivy image  --format table -o trivy-fs-report.html  rajdeepsingh642/php-app:latest ."
            }
        }
             stage('Docker image push') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker-hub') {
                    sh "docker push rajdeepsingh642/php-app:latest"
                    
                       }
                }
             
            }
        }
         
          stage('Docker Run') {
            steps {
               sh "docker run -d -p 8080:80 rajdeepsingh642/php-app:latest"
            
        }
    
     } 
  
   }
}
   
