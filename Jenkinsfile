pipeline {
  agent any
  tools{
    maven 'maven'
  }

  stages{

    stage('build jar'){
      steps{
        script{
          echo "building application artifact.........."
          sh "mvn package"
        }
      }
    }

    stage("build image"){
      steps{
        script{
          echo "building application into docker image......."
          sh 'docker build -t nanaot/java-app:r4 .'

        }
      }
    }

    stage("push image"){
      steps{
        script{
          echo "authenticating and pushing image to private registry....."
          withCredentials([usernamePassword(credentialsId: "docker-credentials", passwordVariable: "PASS", usernameVariable: "USER")]){
            sh 'echo $PASS | docker login -u $USER --password-stdin'
            sh 'docker push nanaot/java-app:r4'
          }

        }
      }
    }
  }
}