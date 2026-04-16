pipeline {
    agent any
    
    environment {
    	LANG='en_US.UTF-8'
    	LC_ALL='en_US.UTF-8'
    }

    tools {
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/narasimhaa44/MavenWebAppPipelineWithAnsible.git'
            }
        }

        stage('Build WAR') {
            steps {
                    sh 'mvn clean package' 
            }
        }
        
        stage('Archive') {
        	steps {
        		archiveArtifacts artifacts: 'target/*.war , fingerprint:true'
        	}
        }
        stage('Deploy to Tomcat') {
            steps {
               sh 'mvn clean package'
               sh 'ansible-playbook playbook.yml -i hosts.ini'      
            }
        }

    }

    post {
        success {
            echo '✅ Deployment to Tomcat successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
