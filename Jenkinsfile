pipeline {
  agent {
    kubernetes {
      yamlFile 'KubernetesPod.yaml'
    }
  }
  stages {
    stage('Checkout') {
	    steps {
		  checkout scm    
	    }      
    } 
    
    stage('Build a Maven project') {
	    steps {
                git 'https://github.com/jenkinsci/kubernetes-plugin.git'
		container('maven') {
	        echo "1.maven build"
                sh 'mvn clean install -Dmaven.test.skip=true'
          }
	    }     
    }
    stage('docker login and push') {
	    steps {
		       container('maven') {
                echo "2.login oc & docker regristry"
                sh "docker login -u 'admin' -p 'Harbor12345' 'http://10.180.249.12:30002'"
                sh "docker build -f src/docker/Dockerfile -t 10.180.249.12:30002/library/test:latest ." 
                sh "docker push 10.180.249.12:30480/library/test:latest"
                }    
	    }
      
    }     
  }
}
