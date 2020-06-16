
podTemplate(
        containers: [
                containerTemplate(name: 'maven', image: 'maven:3.6.0-jdk-8-alpine', ttyEnabled: true, command: 'cat')
   ],
         volumes: [
  		persistentVolumeClaim(mountPath: '/home/jenkins/workspace', claimName: 'pvc', readOnly: false)
  ]) {

  node(POD_LABEL) {
    wrap([$class: 'AnsiColorBuildWrapper', 'colorMapName': 'XTerm', 'defaultFg': 1, 'defaultBg': 2]) {
        // This is the current syntax for invoking a build wrapper, naming the class.
        wrap([$class: 'TimestamperBuildWrapper']) {
         stage('Build a Maven project') {
                 git 'https://github.com/amenaafreen/spring-boot-maven-example-helloworld.git'
                container('maven') {
                           sh '''\
                                export MAVEN_OPTS="-Dmaven.repo.local=/home/jenkins/workspace/.m2/repository" 
                                mvn clean package
                               '''
                }
         }
      }
    }
  }
}
