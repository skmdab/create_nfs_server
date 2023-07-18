pipeline{

    agent any

    stages{
        stage('Checkout the code'){
            steps{
                git branch: 'main',  url: 'https://github.com/skmdab/create_nfs_server.git'
            }
        }

        stage('Creating server'){
            steps{
                sh "sh aws_create.sh"
            }
        }

        stage('Configuring NFS package into server'){
            steps{
                withCredentials([file(credentialsId: 'pemfile', variable: 'PEMFILE')]) {
		   sh 'ansible-playbook install_nfs_server.yaml --private-key="$PEMFILE"'
		}
            }
        }
    }
}
