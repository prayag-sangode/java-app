pipeline {
    agent any
    stages {
       stage ("Git clone")
        {
            steps {
             //withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')]) {
                //sh("gcloud auth activate-service-account --key-file=${GC_KEY}")
                //sh("gsutil ls")
                sh("git clone https://github.com/prayag-sangode/java-app.git")
                }
       
       stage ("Docker Login | Docker Build | Docker Push")
        {
            steps {
             withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')]) {
                sh("gcloud auth print-access-token | sudo docker login -u oauth2accesstoken --password-stdin https://asia-east1-docker.pkg.dev")
                }
             }
        }
    }    
}
