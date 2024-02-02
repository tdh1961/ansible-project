pipeline {
    agent any

    stages {
        stage('Zip and Push to JFrog Artifactory') {
            steps {
                script {
                    // Create a zip file containing all files except Jenkinsfile
                    sh 'zip -r code.zip * -x Jenkinsfile'
                    
                    // Upload the zip file to JFrog Artifactory
                    sh 'curl -uadmin:AP2y1UiRRbNYAGwPGsz56ztnu46 -T code.zip "http://23.21.35.219:8081/artifactory/ansible-project/code.zip"'
                    sh 'curl -uadmin:AP8gqnnJFGjpmxzN9a1p4zdFjHe -T code.zip "http://54.204.103.152:8081/artifactory/code/code.zip"'
                }
            }
        }
stage('Download Artifact from Jfrog') {
            agent {
                label 'ansible'
            }
            steps {
                script {
                    // Download the zip file from JFrog Artifactory

                     sh 'curl -uadmin:AP2y1UiRRbNYAGwPGsz56ztnu46 -O "http://23.21.35.219:8081/artifactory/ansible-project/code.zip"'
                     sh 'curl -uadmin:AP8gqnnJFGjpmxzN9a1p4zdFjHe -O "http://54.204.103.152:8081/artifactory/code/code.zip"'
                    // Now you can use the downloaded files on the agent
                }
            }
        }
stage('Run playbook') {
            agent {
                label 'ansible'
            }
            steps {
                script {
                    // Unzip ansible-codes.zip
                    sh 'unzip -o code.zip'
                    // Run ansible-playbook from the correct directory
                    dir('code') {
                       sh 'ansible-playbook -i /home/ec2-user/ansible-dev/inventory.yml /home/ec2-user/ansible-dev/play2.yml'
                        
                        
                    }
                }
            }
        }
    }
}
