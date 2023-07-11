pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-creds', url: 'https://github.com/etechDevops/etech-mavenApp.git']])
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
    stage('sonarscanner'){
      steps{
      sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team6codereview \
  -Dsonar.projectName='team6codereview' \
  -Dsonar.host.url=http://ec2-35-163-249-27.us-west-2.compute.amazonaws.com:9000 \
  -Dsonar.token=sqp_234f9247e0a9fa7164dec84b0f683dfd4f4f6961"
      }
    }
  }
}
