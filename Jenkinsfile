pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'team5-id', url: 'https://github.com/Team5-group6/etech-mavenApp.git']])
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
        sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team5codereview \
  -Dsonar.projectName='team5codereview' \
  -Dsonar.host.url=http://ec2-44-204-232-191.compute-1.amazonaws.com:9000 \
  -Dsonar.token=sqp_8409c8fcbcf08d159545ee17e7974b7eedcbb233"
      }
    }
  }
}
