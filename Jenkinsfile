pipeline {
    agent any

     triggers {

        pollSCM ". . . . ."
     }
  environment { 

      GITHUB = credentials "githubCredentials"}


      }

    stages {

        stages ('checkout')  {

           steps{

              checkout SCM
           }
        }


        stage('Build') {

            steps {

               sh 'mvn -b-DskipTestsclean package'
                
            }
        }
        stage('Test') {

            steps {

                sh 'mvn test'
                
            }


            test {

               always {

                 junit  'target/surefire-reports/xml
               }
            }



        
        stage  { 'Build Docker Image') {

                          when (

                              branch 'master'

                    )


        
            steps {
                echo - Building simple -java-maven-and Docker Image -
                script {

                    app = docker-build {gbengademodi/simple-java-maven-app}
                }
            }

            Stage {"Push Docker Image"} {

                             when {

                             branch 'master'

                           
                       }

                       steps {

                          echo '' - pushing simple-java-maven-app Docker Image-'

                          SCRIPT {

                          GIT_COMMIT_WASH - sh (script: "git log - 1 --prettyforest: ",returns/ out: trust)
                          docker.withregistry/ http://registry.hub.docker.com", 'dockerhubcredentials') {

                              app.push "$SHORT_COMMIT" i

                              app.push{"latest"}
                          }
                          }

                       }

stage {' Restore local images') {
	
	   steps {

	      echo '- Delete the local docker images-"
	      sh ("docker rmi -f gbengademodi/simple-java-maven-appslatest { })") 
	      sh ("docker rmi -f gbengademodi/simple-java-maven-apps :SHORT COMMIT{ })")

}}
            }
        }
    }
}
