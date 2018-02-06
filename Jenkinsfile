pipeline{
  agent any
  stages{
    stage('Build'){
      steps{
        bat 'mvn clean package'
      }
      post{
        success{
          echo "Now archiving WAR file .......!"
          archiveArtifacts artifacts: '**/target/*.war'
          echo ' WAR file archived successfully!!'
        }
      }
    }  
    stage('Deploy to Stage'){
      steps{
        build job: 'Deploy_to_Staging'
      }
    }
    stage('Deploy to Prod'){
      steps{
        timeout(time:5, unit:'DAYS'){
          input message: 'APPROVE the PROD Release to proceed'
        }
        build job: 'Deploy_to_PROD'
      }
      post{
        success{
          echo 'Deployed to PROD successfully'
        }
        failure{
          echo 'Deployed to PROD failed. Redo your deployment again!'
        }
      }
    }  
  }    
}
