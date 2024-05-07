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
      parallel {
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
              archiveArtifacts '**/target/*.jar'
            }

          }
        }

        stage('Voting Image B&P') {
          agent any
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                def commitHash = env.GIT_COMMIT.take(7)
                def dockerImage = docker.build("initcron/sysfoo:${commitHash}", "./voting")
                dockerImage.push()
                dockerImage.push("latest")
                dockerImage.push("dev")
              }
            }

          }
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