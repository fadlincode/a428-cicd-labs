node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval'){
            input message: 'Lanjut ke tahap Deploy? (Klik "Proceed untuk lanjutkan")'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            sh './jenkins/scripts/kill.sh'
            
            // sleep 60s
            sleep 60
            echo 'Deploy success'
        }
    }
    
}