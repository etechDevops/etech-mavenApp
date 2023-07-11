pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'rnfor', url: 'https://github.com/etechDevops/etech-mavenApp.git']])
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
  -Dsonar.host.url=http://ec2-35-90-225-216.us-west-2.compute.amazonaws.com:9000 \
  -Dsonar.token=sqp_2c2538ba7976bfa58ade95dc55727e0def581cf9"
      }
    }
  }
}
