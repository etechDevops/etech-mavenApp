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
    // stage('2-cleanws'){
    //   steps{
    //     sh 'mvn clean'
    //   }
    // }
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
    stage('5-maven-deploy'){
      steps{
      sh "scp -i key /var/lib/jenkins/workspace/maven-build-job/MavenEnterpriseApp-web/target/MavenEnterpriseApplication.war ubuntu@54.245.156.251:/opt/tomcat/apache-tomcat-9.0.78/webapps"
      }
    }
  }
}
