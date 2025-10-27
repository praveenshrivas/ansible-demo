pipeline {
  agent any

  environment{
    ANSIBLE_HOST_KEY_CHECKING = 'False'
  }

  stages{
    stage('Clone the Repo'){
      steps{
        git branch: 'main', url: 'https://github.com/praveenshrivas/ansible-demo.git'
      }
    }
    stage('Run the Ansible Playbook'){
      steps{
        ansiblePlaybook{
          playbook:'playbook.yml',
          inventory:'hosts.ini',
          credentialsId:'ec2-ssh-key'
        }
      }
    }
  }
}
