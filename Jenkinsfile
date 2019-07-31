pipeline {
  agent none
  triggers {
    cron('0/20 * * * * ? ') // 代表此刻开始开始，每20s执行一次
  }
  stages {
    stage('Checkout') {
	    agent any
	    steps {
		checkout scm    
	    }      
    } 
    
    stage('Build a Maven project') {
	    agent { docker 'maven:3-alpine' }
	    steps {		
	        echo "1.maven build"
                sh 'mvn clean install -Dmaven.test.skip=true'                
	    }
      
    }
    stage('docker login and push') {
	    agent { docker 'docker:latest' }
	    steps {		
                echo "2.login oc & docker regristry"
                sh "docker login -u 'admin' -p 'Harbor12345' 'http://10.180.249.12:30002'"
                sh "docker build -f src/docker/Dockerfile -t 10.180.249.12:30002/library/test:latest ." 
                sh "docker push 10.180.249.12:30480/library/test:latest"                   
	    }
      
    }     
  }
}	
