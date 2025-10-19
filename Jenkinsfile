pipeline {
  agent any
  
  stages {
    stage('checkout') {
     steps {
       git url: 'https://github.com/Saikumar-Pamulaparthi/jenkins-java-project.git'
     }
    }
    stage('Code Quality-Sonarqube') {
     steps {
       withSonarQubeEnv('SonarQubeServer') {
         sh 'mvn clean verify sonar:sonar'
       }
     }
    }
    stage('Build Code') {
     steps {
       sh 'mvn clean package -DskipTests'
     }
    }
    stage('Deployment') {
     steps {
       sh 'cp /var/lib/jenkins/workspace/webhook/target/NETFLIX-1.2.2.war /var/www/html/'
     }
    }

   post {
    success {
      echo 'Pipeline Executed Successfully'
    }
    failure {
      echo 'Build Failed, Please check Jenkins logs '
    }
   }
