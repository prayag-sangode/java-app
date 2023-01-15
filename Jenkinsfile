pipeline {
    agent any
    stages {
         stage ("Docker Login, Build & Push")
            {
            steps {
             withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')]) {
                sh("gcloud auth print-access-token | sudo docker login -u oauth2accesstoken --password-stdin https://asia-east1-docker.pkg.dev")
                }
             }
        }
    }    
}
