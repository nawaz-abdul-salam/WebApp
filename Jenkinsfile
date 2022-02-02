pipeline {
  agent any
  stages {
    stage('Dev Build') {
      steps {
        echo 'Maven Build Done Locally ..'
        echo 'Unit tests executed'
      }
    }

    stage('Deploy to QA') {
      steps {
        echo 'Deploy to QA Env'
        echo 'Notify QA by Email'
      }
    }

    stage('Ui Testing (Smoke)') {
      parallel {
        stage('Ui Testing (Smoke)') {
          steps {
            echo 'Selenium Tests (Smoke)'
          }
        }

        stage('API Tests (Smoke)') {
          steps {
            echo 'Run Rest Assured Tests'
          }
        }

        stage('Performance Tests') {
          steps {
            echo 'Run JMeter tests'
          }
        }

      }
    }

    stage('Deploy to UAT') {
      steps {
        echo 'Deploy to UAT (AWS)'
        echo 'Notify the UAT users'
        input 'Do you want to certify?'
        jiraComment(issueKey: 'S04-83', body: 'Jenkins Completed Testing and about to start UAT deployment')
      }
    }

    stage('Certify UAT') {
      when {
        branch 'master'
      }
      steps {
        echo 'Manual Certify'
        input 'Do you want to certify?'
      }
    }

    stage('Prod Deploy') {
      when {
        branch 'master'
      }
      steps {
        echo 'Deploy to Prod'
      }
    }

  }
}