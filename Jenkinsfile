pipeline {
  agent any

  options {
    skipStagesAfterUnstable()
  }

  stages {
    stage('Checkout Source Code') {
      steps {
        git branch: 'main', url: 'git@github.com:Madr8/springboot-jenkins-midterm.git'
      }
    }

    stage('Test') {
      steps {
        sh 'git --version'
        sh 'mvn --version'
        sh 'mvn clean test'
      }
    }

    stage('Build and Package') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Archive Artifacts') {
      steps {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
  }

  post {
    always {
      echo 'Pipeline finished.'
    }
    success {
      echo 'Build successful!'
    }
    failure {
      echo 'Build failed!'
    }
  }
}
