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
  }
}