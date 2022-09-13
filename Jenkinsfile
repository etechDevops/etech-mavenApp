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

        steps{
            sh 'mvn test'
        }
    }
    stage('codequality'){
      steps{
         sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=felix-pipeline \
  -Dsonar.host.url=http://ec2-18-209-46-117.compute-1.amazonaws.com:9000 \
  -Dsonar.login=sqp_5e2c946cdf88f7cf7973fb26a749e0ba88465b30'
      }
    }

