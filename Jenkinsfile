pipeline {
    agent any
    stages {
       stage ("List GCS Buckets")
        {
            steps {
             withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')]) {
                sh("gcloud auth activate-service-account --key-file=${GC_KEY}")
                sh("gsutil ls")
                sh("gcloud auth print-access-token | sudo docker login -u oauth2accesstoken --password-stdin asia-east1-docker.pkg.dev")
                sh("sudo docker info")
                }
             }
        }
       
    stage ("Docker Auth")
        {
            steps {
             withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')]) {
                sh("gcloud auth configure-docker asia-east1-docker.pkg.dev")
                sh("sudo docker info")
                }
             }
        }
    }    
}
