pipeline {

    agent any 

    stages {

        stage (' soanr quality check') {

            steps {
            
                script {
                    
                   withSonarQubeEnv(credentialsId: 'sonar-token') {
                   
                   sh 'mvn clean package -X sonar:sonar'
                 

                   }
                }
            }
        }

        stage ('Quality gate status') {

            steps {

                script {

                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }

        stage ('docker image build & push into nexus repo') {

            steps {

                scripts {

                    
                }
            }
        }
    }
}
