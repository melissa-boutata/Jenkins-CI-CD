pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        powershell 'C:\\gradle-5.6-bin\\gradle-5.6\\bin\\gradle build'
        powershell 'C:\\gradle-5.6-bin\\gradle-5.6\\bin\\gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
      }
    }

  }
}