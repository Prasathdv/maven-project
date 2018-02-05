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
        }
      }
    }  
  
  }    
}
