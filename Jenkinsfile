pipeline {
  agent none
  stages {
    stage('voting-build') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17-alpine'
        }

      }
      steps {
        echo 'compiling voting app..'
        dir(path: 'voting') {
          sh 'mvn compile'
        }

      }
    }

    stage('voting-test') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17-alpine'
        }

      }
      steps {
        echo 'compiling voting app..'
        dir(path: 'voting') {
          sh 'mvn clean test'
        }

      }
    }

    stage('voting-package') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17-alpine'
        }

      }
      steps {
        echo 'compiling voting app..'
        dir(path: 'voting') {
          sh 'mvn package -DskipTests'
          archiveArtifacts(artifacts: '**/target/*.jar', followSymlinks: false)
        }

      }
    }

  }
  tools {
    maven 'Maven 3.9.6'
  }
  post {
    always {
      echo 'pipeline run completed....'
      
    }

  }
}
