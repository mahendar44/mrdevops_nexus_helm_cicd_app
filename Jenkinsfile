pipeline {

    agent any 
    environment {
       
        VERSION = "${env.BUILD_ID}"
    }

    stages {

        stage (' soanr quality check') {

            
            steps {
            
                script {
                    
                   withSonarQubeEnv(credentialsId: 'sonar-token') {
                   
                   sh 'mvn clean package sonar:sonar'
                 

                   }
                }
            }
        }


        stage ('docker image build & push into nexus repo') {

            steps {

                scripts {

                   withCredentials([string(credentialsId: 'nexus-passwd', variable: 'nexus-creds')]) {

                   sh '''
                    docker build -t 54.81.45.20:8083/springapp:${VERSION} .

                    docker login -u admin -p $nexus-passwd 54.81.45.20:8083

                    docker push 54.81.45.20:8083/springapp:${VERSION}

                    docker rmi 54.81.45.20:8083/springapp:${VERSION}
                   '''
                   } 
                }
            }
        }
        
    }
}
