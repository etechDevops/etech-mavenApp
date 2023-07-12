pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        clone repo
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
      post{
        success{
          echo "Archive the artifacts"
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
      stage('4-Deploy to tomcat server'){
      steps{
        sh 'deploy adapters: [tomcat9(credentialsId: 'rudolph', path: '', url: 'http://ec2-54-184-91-175.us-west-2.compute.amazonaws.com:8080/')], contextPath: null, war: '**/*.war''
      }
    }
  }
}
