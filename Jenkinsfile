pipeline {
  agent any
  // Polling is allowed by the brief (webhook not required)
  triggers { pollSCM('H/5 * * * *') }

  stages {
    stage('Build') { steps { echo 'Build — e.g., Maven/Gradle/npm' } }
    stage('Unit and Integration Tests') { steps { echo 'Unit & Integration Tests — e.g., JUnit/Jest/Mocha' } }
    stage('Code Analysis') { steps { echo 'Static analysis — e.g., SonarQube/ESLint/Checkstyle' } }
    stage('Security Scan') { steps { echo 'Security scan — e.g., OWASP Dependency-Check/Snyk/npm audit' } }
    stage('Deploy to Staging') { steps { echo 'Deploy to staging — e.g., Docker/SSH/AWS EC2' } }
    stage('Integration Tests on Staging') { steps { echo 'E2E/system tests — e.g., Selenium/Cypress' } }
    stage('Deploy to Production') { steps { echo 'Deploy to production — e.g., Ansible/K8s/CodeDeploy' } }
  }
}
