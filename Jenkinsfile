pipeline {
    agent any
    environment {
        SSH_CREDENTIALS_ID = 'ssh_key_for_debian_1'
        REMOTE_HOST = '192.168.1.50'
        REMOTE_USER = 'minheagle'
        REMOTE_DIR = '/home/minheagle/homelab/tutorial'
    }
    triggers {
        githubPush()
    }
    stages {
        stage('Pull Code') {
            steps {
                script {
                    sshagent([SSH_CREDENTIALS_ID]) {
                        sh "ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST} 'cd ${REMOTE_DIR} && git pull'"
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Code updated successfully on the remote server!'
        }
        failure {
            echo 'Failed to update code on the remote server!'
        }
    }
}
