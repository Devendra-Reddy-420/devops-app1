pipeline {
    agent any
    environment {
        WAR_FILE = 'devops-app.war'
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World-Jenkins Pipeline'
            }
        }
        stage("Maven Build"){
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Tomcat-dev"){
            steps {
                script {
                    ansiblePlaybook(
                        playbook: 'deploy_war.yml',
                        inventory: 'inventory/ec2_hosts',
                        extras: "-e war_file=${env.WAR_FILE}"
                    )
                }
            }
        }
    }
}
