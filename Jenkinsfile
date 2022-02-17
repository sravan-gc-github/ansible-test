pipeline {
    //agent any
    agent {
        docker { 
            image 'sravangcpdocker/terraform:7'
            args '-u root:sudo -v $HOME/workspace/myproject:/myproject'
        }
    }
    environment {
   ANSIBLE_PRIVATE_KEY=credentials('ansible-key') 
  }

    stages {
        stage('ansible') {
            steps {
                sh "ansible --version"
                //sh "rm -rf *"
                sh "git clone https://github.com/sravan-github/ansible-test.git"
                //sh "cd ansible-test && chmod 777 play.yml && chmod 600 key && ls -ltr"
                //sh 'cd ansible-test && ansible-galaxy collection install -r requirements.yml'
                sh 'cd ansible-test && ansible-playbook -i hosts --private-key=$ANSIBLE_PRIVATE_KEY play.yml'
               // sh "cd ansible-test && ansible-playbook play.yml -i hosts --private-key key"
            }
        }
    }
    post {
        always {
        	cleanWs deleteDirs: true
        }
    }
}
