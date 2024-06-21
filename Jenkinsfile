#!/user/bin/env groovy

@Library('shared-library')_
pipeline{
  agent any
  tools{
    maven 'maven-3.1'
  }

  stages{

    stage('version increment'){
      steps{
        script{
          echo 'incrementing application version....'
          sh "mvn build-helper:parse-version versions:set \
            -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} versions:commit"
          def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
          def version = matcher[0][1]
          env.IMAGE_NAME = "$version-$BUILD_NUMBER"
        }
      }
    }

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
          buildImage "nanaot/java-app:$IMAGE_NAME"
          dockerLogin()
          pushImage "nanaot/java-app:$IMAGE-NAME"
        }
      }
    }
  }

}