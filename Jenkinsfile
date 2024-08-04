pipeline {
  agent any
  stages {
    stage('Install AWS CLI') {
      steps {
        script {
          if (sh(script: 'which aws', returnStatus: true) != 0) {
            sh 'curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"'
            sh 'unzip awscliv2.zip'
            sh './aws/install'
          }
        }

      }
    }

    stage('Configure AWS Credentials') {
      steps {
        script {
          sh """
          mkdir -p ~/.aws
          echo '[default]' > ~/.aws/credentials
          echo 'aws_access_key_id=${AWS_ACCESS_KEY_ID}' >> ~/.aws/credentials
          echo 'aws_secret_access_key=${AWS_SECRET_ACCESS_KEY}' >> ~/.aws/credentials
          echo '[default]' > ~/.aws/config
          echo 'region=${AWS_REGION}' >> ~/.aws/config
          """
        }

      }
    }

    stage('Launch EC2 Instance') {
      steps {
        script {
          sh """
          aws ec2 run-instances \
          --image-id ami-0abcdef1234567890 \
          --count 1 \
          --instance-type t2.micro \

          """
        }

      }
    }

  }
  environment {
    AWS_REGION = 'us-west-2'
  }
}