pipeline {
    agent any

    environment {
        S3_BUCKET_NAME = 'bucketforjenkinss' // The name of your S3 bucket
        REGION = 'us-east-1' // Region where your S3 bucket is located
    }

    stages {
        stage('Clone Repository') {
            steps {
                // This step will clone your Git repository containing the website code.
                git 'https://github.com/MalikSayyed/react-app-new.git'
            }
        }
        
        stage('Build') {
            steps {
                // If you're using a static website, you might not need to build anything.
                // But if you need to, this is where you would build your website (e.g., run npm build for a React app).
                echo 'Building your website...'
            }
        }

        stage('Deploy to S3') {
            steps {
                script {
                    // Using the credentials stored in Jenkins
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-credentials']]) {
                        // This step uploads all files in the current directory (your website files) to your S3 bucket
                        sh """
                        aws s3 sync . s3://${S3_BUCKET_NAME}/ --region ${REGION} --delete
                        """
                    }
                }
            }
        }
    }
}