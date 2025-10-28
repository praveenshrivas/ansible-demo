pipeline {
  agent any

  environment{
    ANSIBLE_HOST_KEY_CHECKING = 'False'
  }

  stages{

    stage('Copy EC2 Instance From the Artifacts'){
      steps{
        copyArtifacts(
          projectName: 'Terraform-Demo',
          selector: lastSuccessful()
        )
        sh 'cat ec2_ip.txt'
      }
    }

     stage('Generate Dynamic Inventory'){
      steps{
        sh '''
        echo "[demo]" > hosts.ini
        echo "$(cat ec2_ip.txt) ansible_user=ec2-user" >> hosts.ini
        cat hosts.ini
        '''
      }
    }
    
    stage('Clone the Repo'){
      steps{
        git branch: 'main', url: 'https://github.com/praveenshrivas/ansible-demo.git'
      }
    }
    stage('Run the Ansible Playbook'){
      steps{
        ansiblePlaybook(
          playbook: 'playbook.yml',
          inventory: 'hosts.ini',
          credentialsId: 'ec2-ssh-key'
        )
      }
    }
  }
}
