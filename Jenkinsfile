pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: '']]])git@github.com:olubunmi-devops/etech-mavenApp-1.git
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
    stage('code quality'){
      steps{
        sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team3-pipeline-olu \
  -Dsonar.host.url=http://ec2-54-146-99-49.compute-1.amazonaws.com:9000 \
  -Dsonar.login=sqp_087fc78952f1001ea5644c41268266a296c768b3'
      }
    }
        } 
    }
  
  