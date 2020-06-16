
podTemplate(
        containers: [
                containerTemplate(name: 'maven', image: 'maven:3.6.0-jdk-8-alpine', ttyEnabled: true, command: 'cat')
   ],
         volumes: [
  		persistentVolumeClaim(mountPath: '/home/jenkins/workspace', claimName: 'pvc', readOnly: false)
  ]) {
  ansiColor('xterm') {
  node(POD_LABEL) {
          
         stage("\u001B[31m Build a Maven project \u001B[0m") {
                git 'https://github.com/amenaafreen/spring-boot-maven-example-helloworld.git'
                container('maven') {
                           sh '''  
                                printf "\\033[1;32m"
                                export MAVEN_OPTS="-Dmaven.repo.local=/home/jenkins/workspace/.m2/repository" 
                                mvn clean package 
                                printf "\\033[0m"
                              '''
                }
         }
      }
  }
}
