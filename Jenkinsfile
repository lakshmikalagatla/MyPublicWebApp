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
           docker tag jenkins-pipeline sivadockerlakshmi/jenkins-pipeline:latest
        """)
     }
     }
     stage('Push Container'){
   steps {
     echo "Workspace is $WORKSPACE"
     sh(script: """
       docker login -u=$REGISTRY_AUTH_USR -p=$REGISTRY_AUTH_PSW
       docker push sivadockerlakshmi/jenkins-pipeline:latest
     """)
      }
     }
    stage('Deployment'){
           steps {
                   sh(script: 'gcloud init')
                   sh(script: 'gcloud container clusters create cluster-1 --num-nodes=3 --zone=us-west4-c')
           }
       }
    }   
   }
