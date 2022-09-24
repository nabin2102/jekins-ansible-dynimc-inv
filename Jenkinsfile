

pipeline {
  agent { 
  label 'ansible'
  }
  environment {
   AWS_EC2_PRIVATE_KEY=credentials('ec2-private-key') 
  }
  
  stages {
    
    //Get the Code from GitHub Repo
    stage('CheckOutCode'){
      steps{
        stage('CheckOutCode'){
      steps{
        git credentialsId: 'ff0c6339-c067-4d0d-95c8-a0b138ed965e', url: 'https://github.com/nabin2102/jekins-ansible-dynimc-inv'
      }
    }
      }
    }
     
    //Run the playbook
    stage('RunPlaybook') {
      steps {
        //List the dymaic inventory just for verification
        sh "ansible-inventory --graph -i inventory/aws_ec2.yaml"
        //Run playbook using dynamic inventory & limit exuection only fo tomcatservers.
        sh "ansible-playbook -i inventory/aws_ec2.yaml  playbooks/tomcat-setup.yaml -u ec2-user --private-key=$AWS_EC2_PRIVATE_KEY --limit tomcatservers --ssh-common-args='-o StrictHostKeyChecking=no'"
      }
    }
  
  }//stages closing
}//pipeline closing
