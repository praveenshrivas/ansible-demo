pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/praveenshrivas/ansible-demo.git'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                ansiblePlaybook(
                    playbook: 'playbook.yml',
                    inventory: 'hosts.ini',
                    credentialsId: 'ec2-ssh-key'
                )
            }
        }
    }
}
