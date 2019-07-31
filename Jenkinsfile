podTemplate(containers: [
  containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat')
  ]) {

  node(POD_LABEL) {
    stage('Build a Maven project') {
      container('maven') {
          sh 'mvn clean install -Dmaven.test.skip=true '
      }
    }
  }
}
