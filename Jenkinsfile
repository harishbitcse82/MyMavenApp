pipeline {
    agent any  // Use any available agent

    tools {
        maven 'Maven'  // Ensure this matches the name configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/harishbitcse82/MyMavenApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven build
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'  // Run unit tests
            }
        }

        
        
       stage('Deploy') {
            steps {
                // Deploy the JAR file (Copy to a remote server)
                sh 'scp target/MyMavenApp-1.0-SNAPSHOT.jar harish@localhost:/~/applications/deploy/'
            }
        }
        stage('Run Application') {
            steps {
                // Start the JAR application on the remote server
                sh 'ssh harish@localhost "nohup java -jar /~/applications/deploy/MyMavenApp-1.0-SNAPSHOT.jar > /dev/null 2>&1 &"'
            }
        }

        
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

