pipeline {
   agent any

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
     dir("$WORKSPACE") {
        echo "$GIT_BRANCH"
          docker.withRegistry('','DockerHub') {
             }
      }
    }   
   }
}
}
