pipeline {     
    agent any      

    environment {          
        GAR_LOCATION = 'asia-south1-docker.pkg.dev'         
        PROJECT_ID = 'milan-dev-451317'           
        REPOSITORY = 'jenkins-cicd-stack'          
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
                        def latestTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/java-backend:latest"
                        def newTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/java-backend:new"

                        sh """  
                            set -e                           
                            docker build -t ${latestTag} -t ${newTag} -f Dockerfile .                            
                            docker push ${latestTag}                         
                            docker push ${newTag}                         
                        """                     
                    }                 
                }             
            }         
        }          

        stage('Build and Push Python Backend') {             
            steps {                 
                dir('flask') {                     
                    script {                         
                        def latestTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/python-backend:latest"
                        def newTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/python-backend:new"

                        sh """  
                            set -e                           
                            docker build -t ${latestTag} -t ${newTag} .                            
                            docker push ${latestTag}                         
                            docker push ${newTag}                         
                        """                     
                    }                 
                }             
            }         
        }          

        stage('Build and Push React Frontend') {             
            steps {                 
                dir('react-todo') {                     
                    script {                         
                        def latestTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/react-frontend:latest"
                        def newTag = "${GAR_LOCATION}/${PROJECT_ID}/${REPOSITORY}/react-frontend:new"

                        sh """  
                            set -e                           
                            docker build -t ${latestTag} -t ${newTag} .                            
                            docker push ${latestTag}                         
                            docker push ${newTag}                         
                        """                     
                    }                 
                }             
            }         
        }     
    } 
}
