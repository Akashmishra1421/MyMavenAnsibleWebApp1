pipeline {
    agent any  // Use any available agent
    
    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }  // This is required if UTF-8 is necessary, as mentioned

    tools {
        maven 'Maven'  // Ensure this matches the name configured in Jenkins
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Hemavathipcse/MavenAnsibleWebApp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven build
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                // No need to rebuild here if it's already done in the 'Build' stage
                sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
            }
        }
    }
}
