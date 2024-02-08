// pipeline {
//     agent {
//         docker {
//             image 'node:16-buster-slim'
//             args '-p 3000:3000'
//         }
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'npm install'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh './jenkins/scripts/test.sh'
//             }
//         }
//     }
// }

node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000'){
        stage('Build'){
            sh 'npm install'
        }

        stage('Test'){
            sh './jenkins/scripts/test.sh'
        }

        stage('Manual Approval'){
            input message: 'Lanjutkan ke tahap Deploy?'
        }

        stage('Deploy'){
            sh './jenkins/scripts/deliver.sh'
            echo 'Starting pipeline sleep (1 minute)...'
            echo 'React-App akan dapat ditest selama 1 menit sebelum proses pipeline berjalan kembali dan selesai!'
            sh 'sleep 1m'
            sh './jenkins/scripts/kill.sh'
        }
    }
}