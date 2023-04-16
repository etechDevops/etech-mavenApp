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
      sh "mvn clean verify sonar:sonar\
  -Dsonar.projectKey=team5project\
  -Dsonar.projectName='team5project'\
  -Dsonar.host.url=http://ec2-107-22-47-64.compute-1.amazonaws.com:9000\
  -Dsonar.token=sqp_2c6fd5c10664b2156ff587276f5c07d58bfec9f2"
      }
    }
  }
}
