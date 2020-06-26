pipeline {
   agent any
   environment {
    REGISTRY_AUTH = credentials("DockerHub")
   }
   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
     stage('Docker Build') {
     steps {
	sh(script: 'docker images -a')
        sh(script: """
           #cd MyPublicWebApp/
           docker images -a
           docker build -t jenkins-pipeline .
           cd ..
        """)
     }
     }
     stage('Push Container'){
   steps {
     echo "Workspace is $WORKSPACE"
     sh(script: """
       docker login -u=$REGISTRY_AUTH_USR -p=$REGISTRY_AUTH_PSW ${env.REGISTRY_ADDRESS}
       docker push jenkins-pipeline:latest
     """)  
      }
     }
    }   
   }
