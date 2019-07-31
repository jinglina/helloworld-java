pipeline {
  agent {
    kubernetes {
      label podlabel
      yaml """
kind: Pod
metadata:
  name: jenkins-slave      
spec:
  containers:
  - name: jnlp
    env:
    - name: CONTAINER_ENV_VAR
      value: jnlp
  - name: maven
    image: maven:3.3.9-jdk-8-alpine
    command:
    - cat
    tty: true
    env:
    - name: CONTAINER_ENV_VAR
      value: maven
  - name: busybox
    image: busybox
    command:
    - cat
    tty: true
    env:
    - name: CONTAINER_ENV_VAR
      value: busybox 
"""      
    }
  }  
  triggers {
    cron('0/20 * * * * ? ') // 代表此刻开始开始，每20s执行一次
  }
  stages {
    stage('Checkout') {
	    steps {
		checkout scm    
	    }      
    } 
    
    stage('Build a Maven project') {
	    steps {
		container('maven') {
	        echo "1.maven build"
                sh 'mvn clean install -Dmaven.test.skip=true'
                }
	    }
      
    }
    stage('docker login and push') {
	    steps {
		container('docker') {
                echo "2.login oc & docker regristry"
                sh "docker login -u 'admin' -p 'Harbor12345' 'http://10.180.249.12:30002'"
                sh "docker build -f src/docker/Dockerfile -t 10.180.249.12:30002/library/test:latest ." 
                sh "docker push 10.180.249.12:30480/library/test:latest"
                }    
	    }
      
    }     
  }
}	
