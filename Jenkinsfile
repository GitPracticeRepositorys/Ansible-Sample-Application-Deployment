pipeline {
    agent {
        node {
            label 'Ansible'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                ansiblePlaybook([
                    playbook: 'deploy.yml',
                    inventory: 'hosts',
                    extras: '-e "app_version=target/onlinebookstore-1.0.0.jar"'
                ])
            }
        }
    }
}

def ansiblePlaybook(Map<String, Object> options) {
    def args = options.collect { k, v -> "-${k} ${v}" }.join(' ')
    sh "ansible-playbook ${args}"
}
