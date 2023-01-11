pipeline {
    agent any
    
    tools
    {
       maven "MAVEN_HOME"
    }
     
    stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', credentialsId: 'githubId', url: 'https://github.com/devops4solutions/CI-example.git'
             
          }
        }
         stage('Tools Init') {
            steps {
                script {
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
               def tfHome = tool name: 'ANSIBLE'
                env.PATH = "${tfHome}:${env.PATH}"
                 
                    
            }
            }
        }
     
        
         stage('Execute Maven') {
           steps {
             
                bat 'mvn clean install'             
          }
        }
        
        
         
        
        
        
        stage('Ansible Deploy') {
             
            steps {
                 
             
               
               bat "ansible-playbook main.yml -i inventories/dev/hosts --user jenkins --key-file ~/.ssh/id_rsa"

               
            
            }
        }
    }
}
