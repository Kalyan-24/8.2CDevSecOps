pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Kalyan-24/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'cmd /c npm test || exit /b 0'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        bat 'cmd /c npm run coverage || exit /b 0'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        bat 'cmd /c npm audit || exit /b 0'
      }
    }
  }

  post {
    always {
      emailext(
        to: 's224875746@deakin.edu.au',
        subject: "Build ${currentBuild.fullDisplayName}: ${currentBuild.currentResult}",
        body: """Hello,

The pipeline for ${env.JOB_NAME} finished with status: ${currentBuild.currentResult}.

Check the console log here: ${env.BUILD_URL}console

Thanks,
Jenkins
""",
        attachLog: true
      )
    }
  }
}
