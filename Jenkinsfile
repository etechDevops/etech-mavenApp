pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'jenkinsgit', url: 'https://github.com/YomiPounds/etech-mavenApp.git']]])      
      }
    }
    stage('2-cleanws'){
      steps{
        sh 'mvn clean'
      }
    }
    stage('3-mavenbuild'){
      steps{
        sh 'mvn package'
      }
    }
    stage('unittest'){
      steps{
        sh 'mvn test'
        }
    }
    stage('code coverage sona'){
      steps{
        sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=maven-jenkins-pipeline \
  -Dsonar.host.url=http://ec2-3-139-112-86.us-east-2.compute.amazonaws.com:9000 \
  -Dsonar.login=sqp_191cd314b877c4c780f69cabf8567a10539306a3'
      }
    }
  }
}
