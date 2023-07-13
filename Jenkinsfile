pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
          checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'nfor', url: 'https://github.com/etechDevops/etech-mavenApp.git']])
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
    stage('4-unittest'){
        steps{
            sh 'mvn test'
        }
    }
    stage('5-code-quality'){
        steps{
       sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team6-codeQuality-analysis \
  -Dsonar.projectName='team6-codeQuality-analysis' \
  -Dsonar.host.url=http://ec2-52-11-250-251.us-west-2.compute.amazonaws.com:9000 \
  -Dsonar.token=sqp_e35658cb565d76fc713a851988e7d91a314dfc2b'
        }
    }
  }
}
