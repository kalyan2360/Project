pipeline {
    agent any
     environment {
        DOCKER_IMAGE = 'kalyankumar1996/projectdemo' // Replace with your Docker Hub repo name
        DOCKER_TAG = 'latest' // You can set this to dynamic values like ${env.BUILD_NUMBER}
    }

    

    stages {
        stage('Checkout') {
            steps {
                // Clone the Git repository
                 sh 'cd backend'
                git branch: 'main', url: 'https://github.com/kalyan2360/Project.git'
            }
        }

        stage('Build') {
            steps {
                // Run Maven build
                sh 'cd frontend'
                sh 'mvn clean install -DskipTests=true'
            }
        }

      stage('Build2') {
            steps {
                // Run Maven build
                sh 'cd backend'
                sh 'mvn clean install -DskipTests=true'
            }
        }


       
             
     stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }

               stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using credentials
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    }
                }
            }
        }
             
  stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }
    
                   
        stage('Test') {
            steps {
                // Run Maven tests
                sh 'cd backend'
                sh 'mvn test -DskipTests=true'
            }
        }

        stage('Package') {
            steps {
                // Package the application (if not covered in the build step)
                sh 'cd backend'
                sh 'mvn package -DskipTests=true'
            }
        }

        
    }

}
