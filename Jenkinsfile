pipeline {
    agent any

    environment {
        //GOOGLE_CLOUD_KEYFILE = credentials('gcp-credentials')  // Add GCP service account key in Jenkins
        GAR_LOCATION = 'asia-south1-docker.pkg.dev'
        PROJECT_ID = 'milan-dev-451317'  // Replace with your project ID
        REPOSITORY = 'jenkins-cicd-stack'  // Your GAR repository name
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        
        stage('Build and Push Java Backend') {
            steps {
                dir('backend-java') {
                    script {
                        def imageTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/java-app:${BUILD_NUMBER}"
                        sh """
                            set -e
                            docker build -t ${imageTag} .
                            docker tag ${imageTag} ${imageTag}-latest
                            docker push ${imageTag}
                            docker push ${imageTag}-latest
                        """
                    }
                }
            }
        }

        stage('Build and Push Python Backend') {
            steps {
                dir('backend-python') {
                    script {
                        def imageTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/python-app:${BUILD_NUMBER}"
                        sh """
                            set -e
                            docker build -t ${imageTag} .
                            docker tag ${imageTag} ${imageTag}-latest
                            docker push ${imageTag}
                            docker push ${imageTag}-latest
                        """
                    }
                }
            }
        }

        stage('Build and Push Frontend') {
            steps {
                dir('frontend') {
                    script {
                        def imageTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/frontend-app:${BUILD_NUMBER}"
                        sh """
                            set -e
                            docker build -t ${imageTag} .
                            docker tag ${imageTag} ${imageTag}-latest
                            docker push ${imageTag}
                            docker push ${imageTag}-latest
                        """
                    }
                }
            }
        }
    }
}
