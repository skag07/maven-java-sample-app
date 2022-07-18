pipeline {
    agent any

    stages {
        stage('Build'){
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test'){
            steps {
                sh 'mvn test'
            }
        }

        stage('Package'){
            
        steps {
                sh 'mvn package'
           }

         post {
            always {
                junit 'target/surefire-reports/TEST-*.xml'
            }
            success {
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
        
        }

        stage('Deploy'){
            steps {

                withEnv(['JENKINS_NODE_COOKIE=dontKillMe']) {

                sh '& java "-Dserver.port=8001" -jar target/spring-petclinic-2.3.1.BUILD-SNAPSHOT.jar'

                }
            }
        }
    }



}
