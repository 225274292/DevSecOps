pipeline {
  agent any
   // Polling is allowed by the brief (webhook not required)
  triggers { pollSCM('H/5 * * * *') }

  stages {
    stage('Build') { steps { echo 'Task: Compile and package the code'
        echo 'Tool: Maven' } }
    stage('Unit and Integration Tests') {echo 'Task: Run unit and integration tests'
        echo 'Tool: JUnit' } }
    stage('Code Analysis') { steps {  echo 'Task: Static code quality analysis'
        echo 'Tool: SonarQube' } }
    stage('Security Scan') { steps {  echo 'Task: Dependency vulnerability scan'
        echo 'Tool: OWASP Dependency-Check' } }
    stage('Deploy to Staging') { steps { echo 'Task: Deploy artifact to a staging server'
        echo 'Tool: AWS CLI (EC2)' } }
    stage('Integration Tests on Staging') { steps { echo 'Task: End-to-end/system tests on staging'
        echo 'Tool: Selenium' } }
    stage('Deploy to Production') { echo 'Task: Deploy artifact to production'
        echo 'Tool: AWS CodeDeploy' } }
  }
}
