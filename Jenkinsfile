pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Clone the Git repository
                git url: 'https://github.com/GitPracticeRepositorys/Ansible-Sample-Application-Deployment.git'
            }
        }
        stage('Deploy') {
            environment {
                // Set the credentials for the Ansible deployment
                ANSIBLE_USER = credentials('ansible-user')
                ANSIBLE_PASSWORD = credentials('ansible-password')
            }
            steps {
                // Install the Ansible package
                sh 'sudo apt-get update && sudo apt-get install -y ansible'

                // Run the Ansible playbook to deploy the application
                sh 'ansible-playbook -i hosts deploy.yml --extra-vars "ansible_user=$ANSIBLE_USER ansible_password=$ANSIBLE_PASSWORD"'
            }
        }
    }
}
