pipeline{
  agent any 

  tools{
    maven 'Maven 3.9.6'
  }
 
  stages{
    stage("voting-build"){
      steps{
        echo 'compiling voting app..'
        dir('voting'){
          sh 'mvn compile'
        }
      }
    }

    stage("voting-test"){
      steps{
        echo 'compiling voting app..'
        dir('voting'){
          sh 'mvn clean test'
        }
      }
    }

    stage("voting-package"){
      steps{
        echo 'compiling voting app..'
        dir('voting'){
          sh 'mvn package -DskipTests'
        }
      }
    }

    
  }

  post{
    always{
      echo 'pipeline run completed....'
      archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
    }
  }
}
