pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the Git repository
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/amitkumar114/cloudformationdeployment.git']]])
            }
        }
               

        stage('Deploy CloudFormation Stack') {
            steps {
                script {
                    // Run the AWS CLI command to deploy the CloudFormation stack
                   try {
                        sh 'aws cloudformation deploy --stack-name MyEC2Stack --template-file /root/cloudformationdeployment/cf-deployment/ec2-template.yaml --capabilities CAPABILITY_NAMED_IAM'
                    } catch (Exception e) {
                        error("Failed to deploy CloudFormation stack: ${e}")
                    }
                }
            }
        }
    }
}
