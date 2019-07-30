pipeline {
  agent {
    kubernetes {     
        containerTemplate {
          name 'docker'
          image 'docker:latest'
          ttyEnabled true
          command 'cat'
        }
        containerTemplate {
          name 'maven'
          image 'maven:3.3.9-jdk-8-alpine'
          ttyEnabled true
          command 'cat'
        }
      }
  }  
  triggers {
    cron('0/20 * * * * ? ') // 代表此刻开始开始，每20s执行一次
  }
  stages {
    stage('Checkout') {
        checkout scm
    } 
    
    stage('Build a Maven project') {
      container('maven') {
	    echo "1.maven build"
        sh 'mvn clean install -Dmaven.test.skip=true'
      }
    }
    stage('docker login and push') {
      container('docker') {
        echo "2.login oc & docker regristry"
        sh "docker login -u 'admin' -p 'Harbor12345' 'http://10.180.249.12:30002'"
        sh "docker build -f src/docker/Dockerfile -t 10.180.249.12:30002/library/test:latest ." 
        sh "docker push 10.180.249.12:30480/library/test:latest"
      }
    }     
}
