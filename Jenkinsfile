pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        powershell 'C:\\gradle-5.6-bin\\gradle-5.6\\bin\\gradle build'
        powershell 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
        junit 'build/test-results/test/*.xml'
      }
    }

  }
}