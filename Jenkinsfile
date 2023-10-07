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
    stage('codequality'){
        steps{
       sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team7 \
  -Dsonar.projectName='team7' \
  -Dsonar.host.url=http://34.212.154.53:9000 \
  -Dsonar.token=sqp_51b84d6e7e0661a188ca5b8acce8959c9a8745ff'
        }
    }
  }
}
