podTemplate(containers: [
  containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat')
  ]) {

  node(master) {
    stage('Build a Maven project') {
      git 'https://github.com/jinglina/helloworld-java.git'
      container('maven') {
          sh 'mvn -B clean package'
      }
    }
  }
}
