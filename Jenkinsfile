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

    stage('Mail Notification') {
      steps {
        emailext(subject: 'Build notification', body: 'Success or Failure', from: 'hm_boutata@esi.dz', to: 'hm_boutata@esi.dz')
      }
    }

  }
}