pipeline {

    agent any

    parameters {
        booleanParam(name: 'autoApprove', defaultValue: false,
                     description: 'Automatically run apply after generating plan?')
    }

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION    = 'ap-south-1'
    }

    stages {

        stage('Plan') {
            steps {
                sh 'terraform init'
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Apply') {
            when {
                expression { return params.autoApprove }
            }
            steps {
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }
}
