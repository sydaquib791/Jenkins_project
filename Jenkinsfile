pipeline {
    agent any
    
    tools {
        maven 'MAVEN3'
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Jenkins automatically checks out the code before this step runs
                // We just use this stage to visually confirm it on the dashboard
                echo 'Source code checked out successfully from GitHub.'
            }
        }
        
        stage('Build') {
            steps {
                dir('backend') {
                    // Step 4: Compile the code
                    sh 'mvn clean compile'
                    echo 'Backend compiled successfully.'
                }
            }
        }
        
        stage('Test') {
            steps {
                dir('backend') {
                    // Step 5: Automated Tests execute
                    sh 'mvn test'
                    echo 'Automated tests passed successfully.'
                }
            }
        }
        
        stage('Package') {
            steps {
                dir('backend') {
                    // Package the JAR for the Docker build
                    sh 'mvn package'
                }
            }
        }
        
        stage('Docker Build') {
            steps {
                // Step 6: Docker Image built
                // Using the modern 'docker compose' syntax (V2) instead of the old hyphenated version
                sh 'docker compose build'
                echo 'Docker images built successfully.'
            }
        }
        
        stage('Deploy (CD)') {
            steps {
                // Step 7: Deploy the containers
                sh 'docker compose down' // Stops old versions if they exist
                sh 'docker compose up -d' // Starts the new versions in the background
                echo 'Step 8: Application is LIVE!'
            }
        }
    }
}
