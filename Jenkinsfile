pipeline {
  agent 'any'
   tools {
        maven 'MAVEN_HOME'
    }
stages {

   stage('Git Clone'){
       steps {

              echo 'Clonning Start'

              git url: 'https://github.com/shiva-kant/hellorepo.git'

              echo 'Clonning Done'
              }
          }

   stage('MAVEN TASK'){
         steps {
            echo 'MAVEN Start....................'

            sh 'mvn -f HelloCICDIMAGE/pom.xml clean package'
            
            
            
            echo 'MAVEN Done.........................'
               }

         }
 
        stage ('Copying file') {
            steps {
               echo '##################copy start############'
                sh("cp -R /Users/shiva/.jenkins/workspace/hello/HelloCICDIMAGE/target/*.jar /Users/shiva/.jenkins/workspace/hello ")
              sh("cp -R /Users/shiva/.jenkins/workspace/hello/HelloCICDIMAGE/Dockerfile /Users/shiva/.jenkins/workspace/hello ")
              echo   'copy ###########FINIshed###############'
            }
        }
   stage('DOCKER TASK'){
         steps {
            echo 'DOCKER Start....................'

              sh "docker build  -t myimage:${currentBuild.number} . "
              //sh "docker run -d -p 8085:1234 myimage:${currentBuild.number}"
              
            echo 'DOCKER Done.........................'
               }

         }
  stage('DOCKER LOGIN AND PUSH'){
         steps {
            echo 'DOCKER LOGIN Start....................'
           echo "Build number is ${currentBuild.number}"
              sh "docker tag myimage:${currentBuild.number}  shivakant/myimage:${currentBuild.number}"
              sh "docker login -u shivakant -p shiva@docker123"
              sh "docker push shivakant/myimage:${currentBuild.number}"
              
            echo 'DOCKER PUSH DONE.........................'
               }

         }
}

}
