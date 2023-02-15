pipeline {
  agent {
    docker {
      image 'node:14'
    }
  }
  stages {
    stage('Clone repository') {
      steps {
        git branch: 'main',
        url: 'https://github.com/thehasht/PES1UG20CS161_Jenkins.git'
      }
    }
    stage('Install dependancies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build application') {
      steps {
        sh 'npm run build'
      }
    }
    stage('Test application') {
      steps {
        sh 'npm test'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean install'
        echo 'Build Stage Successful'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
        echo 'Test Stage Successful'
        post {
          always {
            juint 'target/surefire-reports/*.xml'
          }
        }
      }
    }
    stage('Deploy') {
      steps {
        sh 'mvn deploy'
        echo 'Deployment Successful'
      }
    }
  }
  post {
    failure {
      echo 'Pipeline failed'
    }
  }
}
