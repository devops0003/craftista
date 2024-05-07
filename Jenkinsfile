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
  }

  post{
    always{
      echo 'pipeline run completed....'
    }
  }
}
