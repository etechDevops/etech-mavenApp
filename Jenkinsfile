pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/etechDevops/etech-mavenApp.git']]])
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
    stage('codequality-analysis'){
      steps{
        sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team3-pipeline \
  -Dsonar.host.url=http://ec2-3-16-56-47.us-east-2.compute.amazonaws.com:9000 \
  -Dsonar.login=sqp_b7a2660c5d38cedd1b10a5f7e779ea83805d8e7a'
      }
    }  
  }
}
