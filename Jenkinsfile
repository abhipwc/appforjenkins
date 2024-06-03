pipeline {
  agent any
  environment {
    APPSYSID = '2a9a363d83a202106edfe3e0deaad3df'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS = 'SeriveNow_Dev_Instance'
    CREDENTIALS_TEST = 'SeriveNow_Test_Instance'
    DEVENV = 'https://dev271975.service-now.com/'
    TESTENV = 'https://dev254810.service-now.com/'
  }
  stages {
    stage('Build') {
      when {
        not {
          branch 'main'
        }
      }
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
      }
    }
    stage('Deploy to Test Environment') {
      when {
        branch 'main'
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS_TEST}", url: "${TESTENV}", appSysId: "${APPSYSID}")
      }
    }
  }
}
