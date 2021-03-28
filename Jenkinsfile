pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts ' archiveArtifacts \'build/libs/*.jar\''
        archiveArtifacts 'archiveArtifacts \'build/docs/javadoc/*\''
        junit 'junit \'build/test-results/test/*.xml\''
      }
    }

  }
}