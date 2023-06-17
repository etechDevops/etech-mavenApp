pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/Mezie123/etech-mavenApp.git']]])
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
  -Dsonar.projectKey=team3-pipeline \
  -Dsonar.projectName='team3-pipeline' \
  -Dsonar.host.url=http://ec2-44-203-55-42.compute-1.amazonaws.com:9000 \
  -Dsonar.token=sqp_72a8fca9ebed64c797cc14c17782ec639a91dfa5"
      }
    }
  }
}
