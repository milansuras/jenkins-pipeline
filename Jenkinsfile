pipeline {     
    agent any      

    environment {          
        GAR_LOCATION = 'asia-south1-docker.pkg.dev'         
        PROJECT_ID = 'milan-dev-451317'           
        REPOSITORY = 'jenkins-cicd-satck'          
        BUILD_NUMBER = "duck"       
    }    

    stages {         
        stage('Checkout') {             
            steps {                 
                checkout scm             
            }         
        }          

        stage('Authenticate Docker') {             
            steps {                 
                withCredentials([file(credentialsId: 'gcp-credentials', variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {                     
                    sh """                         
                        gcloud auth activate-service-account --key-file=${GOOGLE_APPLICATION_CREDENTIALS}                         
                        gcloud auth configure-docker ${GAR_LOCATION} --quiet                     
                    """                 
                }             
            }         
        }          

        stage('Build and Push Java Backend') {             
            steps {                 
                dir('java-springboot') {                     
                    script {                         
                        def imageTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/java-app:${env.BUILD_NUMBER}"                         
                        sh """                             
                            docker build -t ${imageTag} -f Dockerfile .                              
                            docker tag ${imageTag} ${imageTag}                             
                            docker push ${imageTag}                         
                        """                     
                    }                 
                }             
            }         
        }          

        stage('Build and Push Python Backend') {             
            steps {                 
                dir('flask') {                     
                    script {                         
                        def imageTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/python-app:${BUILD_NUMBER}"                         
                        sh """                             
                            set -e                             
                            docker build -t ${imageTag} .                             
                            docker tag ${imageTag} ${imageTag}                             
                            docker push ${imageTag}                         
                        """                     
                    }                 
                }             
            }         
        }          

        stage('Build and Push React Frontend') {             
            steps {                 
                dir('react-todo') {                     
                    script {                         
                        def imageTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/frontend-app:${BUILD_NUMBER}"                         
                        sh """                             
                            set -e                             
                            docker build -t ${imageTag} .                             
                            docker tag ${imageTag} ${imageTag}                             
                            docker push ${imageTag}                         
                        """                     
                    }                 
                }             
            }         
        }     
    } 
}
