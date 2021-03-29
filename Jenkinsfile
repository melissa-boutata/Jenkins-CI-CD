pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        bat 'C:\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle build'
        bat 'C:\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle javadoc'
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
              bat 'C:\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle sonarqube'
            }

            waitForQualityGate true
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
        bat 'C:\\\\gradle-5.6-bin\\\\gradle-5.6\\\\bin\\\\gradle publish'
      }
    }

    stage('Slack Notification') {
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services/', token: 'T01MQLBV9BK/B01SN9TD8UB/d5Savm0klMv69g5lVdks0bvy', channel: 'general', message: 'API Deployee', teamDomain: 'TP Gradle2021')
      }
    }

  }
}