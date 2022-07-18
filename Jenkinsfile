pipeline {
    agent any

    stages {
        
         stage('Quality Scan') {
            steps {
               
            sh "mvn -Dmaven.test.failure.ignore=true clean compile"
               
            sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=demo5 \
  -Dsonar.host.url=http://54.226.50.200 \
  -Dsonar.login=sqp_50bb0b503303ece646f334b8f55375d33625aa6a"

               
            }

            
        }
        
        stage('Build') {
            steps {

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            
             post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
                success {
                    
                    archiveArtifacts 'target/*.jar'
                }
            }
            
        }
        
       
    }
}