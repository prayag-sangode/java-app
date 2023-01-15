pipeline {
    agent any
    stages {
       stage ("List GCS Buckets")
        {
            steps {
             withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')]) {
                sh("gcloud auth activate-service-account --key-file=${GC_KEY}")
                sh("gsutil ls")
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
