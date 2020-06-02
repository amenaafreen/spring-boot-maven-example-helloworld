
podTemplate(label: label,
        containers: [
                containerTemplate(name: 'maven', image: 'maven:3.6.0-jdk-8-alpine', ttyEnabled: true, command: 'cat')
   ],
         volumes: [
  		persistentVolumeClaim(mountPath: '/root/.m2/repository', claimName: 'pvc', readOnly: false)
  ]) {

  node(POD_LABEL) {
    stage('Build a Maven project') {
      git 'https://github.com/amenaafreen/spring-boot-maven-example-helloworld.git'
      container('maven') {
          sh 'mvn -B clean package'
      }
    }
  }
}
