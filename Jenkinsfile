pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        bat 'C:\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle build'
        powershell 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build notification', body: 'Success or Failure', from: 'hm_boutata@esi.dz', to: 'hi_hamdine@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              powershell 'C:\\gradle-5.6-bin\\gradle-5.6\\bin\\gradle sonarqube'
            }

          }
        }

        stage('Test Reporting') {
          steps {
            cucumber '**/*.json'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        powershell 'C:\\gradle-5.6-bin\\gradle-5.6\\bin\\gradle publish'
      }
    }

  }
}