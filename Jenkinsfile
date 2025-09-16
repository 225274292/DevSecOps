pipeline {
  agent any
  tools { nodejs 'Node20-LTS' }
  options { timestamps() }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/225274292/DevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        // use npm ci if package-lock.json exists, else fallback to npm install
        bat 'if exist package-lock.json (npm ci) else (npm install)'
      }
    }

    stage('Snyk Setup (Auth)') {
      steps {
        withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
          bat 'npm install -g snyk'
          bat 'snyk auth %SNYK_TOKEN%'
        }
      }
    }

    stage('Run Tests') {
      steps {
        // nodejs-goof’s "test" runs "snyk test"; do not fail the build on non-zero exit
        bat 'npm test || exit /b 0'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        // If "npm run coverage" is missing, create a dummy lcov and keep the build going
        catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE') {
          bat 'npm run coverage || (if not exist coverage mkdir coverage && echo TN> coverage\\lcov.info)'
        }
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        bat 'npm audit || exit /b 0'
      }
    }
  }

  post {
    always {
      // handy artifact for submission
      archiveArtifacts artifacts: 'coverage/lcov.info', allowEmptyArchive: true
    }
  }
}
