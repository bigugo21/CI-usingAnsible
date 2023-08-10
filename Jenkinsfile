pipeline {
    agent any
    
    tools
    {
       maven "Maven"
    }
     
    stages {
      stage('checkout') {
           steps {
               
             git credentialsId: '4664b63a-18e4-4579-9c07-f6801e95cf27', url: 'https://github.com/bigugo21/CI-usingAnsible'
             
          }
        }
         stage('Tools Init') {
            steps {
                script {
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
               def tfHome = tool name: 'Ansible'
                env.PATH = "${tfHome}:${env.PATH}"
                 sh 'ansible --version'
                    
            }
            }
        }
     
        
         stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        
        
         
        
        
        
        stage('Ansible Deploy') {
             
            steps {
                 
             
               
               sh "ansible-playbook main.yml -i inventories/dev/hosts --user jenkins --key-file ~/.ssh/id_rsa"

               
            
            }
        }
    }
}
