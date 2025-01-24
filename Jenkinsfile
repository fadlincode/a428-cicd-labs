node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            checkout scm
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval'){
            sh 'rm -rf build/'
            
            sh './jenkins/scripts/deliver.sh'

            input message: 'Lanjut ke tahap Deploy? (Klik "Proceed untuk lanjutkan")'
        }
        stage('Deploy') {
            sh './jenkins/scripts/kill.sh'
            
            sshagent(['SSH_GCP_JENKINS']) {
                sh '''
                echo "Starting deployment to Cloud..."
                scp -o StrictHostKeyChecking=no -r build/ fadlinarsin12@35.226.98.155:~/react-app
                '''
            }
            
            // sleep 60s
            sleep 60
            echo 'Deploy success'
        }
    }
    
}