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
    stage('sonarscanner'){
      steps{
      sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=james1sonaqube \
  -Dsonar.projectName='james1sonaqube' \
  -Dsonar.host.url=http://44.206.227.18:9000 \
  -Dsonar.token=sqp_efdd08d6653d28e0a3956345d49d6871e87d23bb"
      }
    }
  }
}
