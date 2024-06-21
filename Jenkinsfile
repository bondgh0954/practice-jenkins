#!/user/bin/env groovy

@Library('shared-library')_
pipeline{
  agent any
  tools{
    maven 'maven-3.1'
  }

  stages{

    stage('build jar'){
      steps{
        script{
          buildJar()
        }
      }
    }
    stage('building image'){
      steps{
        script{
          buildImage 'nanaot/java-app:70.1'
          dockerLogin()
          pushImage 'nanaot/java-app:70.1'
        }
      }
    }
  }

}