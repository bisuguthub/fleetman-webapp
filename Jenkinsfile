pipeline {
   agent any

   environment {
     SERVICE_NAME = "fleetman-webapp"
     ORGANIZATION_NAME = "fleetman-ci-cd-demo"
     YOUR_DOCKERHUB_USERNAME="virtualpairprogrammers"
     REPOSITORY_TAG="${YOUR_DOCKERHUB_USERNAME}/${ORGANIZATION_NAME}-${SERVICE_NAME}:${BUILD_ID}"
   }

   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'GitHub', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }
      stage('Build') {
         steps {
            sh '''echo No build required for Webapp - it's already built in the /dist directory. This is just to avoid having to configure angular in Jenkins, but usually the build step would be done here.'''
         }
      }

      stage('Build and Push Image') {
         steps {
           sh 'docker image build -t ${REPOSITORY_TAG} .'
         }
      }

      stage('Deploy to Cluster') {
          steps {
            sh 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl apply -f -'
          }
      }
   }
}
