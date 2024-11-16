pipeline {
    agent any

    

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
