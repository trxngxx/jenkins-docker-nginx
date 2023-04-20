pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [[$class: 'CloneOption', depth: 0, noTags: false, reference: '', shallow: false]],
                          submoduleCfg: [],
                          userRemoteConfigs: [[credentialsId: 'github-creds', url: 'https://github.com/my-org/my-repo.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'sudo apt-get update && sudo apt-get install -y nginx'
            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo cp /var/lib/jenkins/workspace/my-job/index.html /var/www/html/'
                sh 'sudo cp /var/lib/jenkins/workspace/my-job/nginx.conf /etc/nginx/nginx.conf'
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}
