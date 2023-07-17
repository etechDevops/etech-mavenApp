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
      post{
        success{
          echo "Archive the artifacts"
          archiveArtifacts artifacts: '**/target/*.war'
        }
      }
    }
      stage('4-Deploy to tomcat server'){
      steps{
        deploy adapters: [tomcat9(credentialsId: 'tomcat-creds2', path: '', url: 'http://18.236.104.120:8080/')], contextPath: null, war: '**/*.war'
      }
    }
  }
}
 
//     stage('5-code-analysis'){
//       steps{
//       sh "mvn clean verify sonar:sonar \
//   -Dsonar.projectKey=team6-codeQuality-analysis \
//   -Dsonar.projectName='team6-codeQuality-analysis' \
//   -Dsonar.host.url=http://ec2-52-11-250-251.us-west-2.compute.amazonaws.com:9000 \
//   -Dsonar.token=sqp_e35658cb565d76fc713a851988e7d91a314dfc2b"
//       }
//     }
//   }
// }
