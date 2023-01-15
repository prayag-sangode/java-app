pipeline {
    agent any
    stages {
         stage ("Docker Login, Build & Push")
            {
            steps {
             withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')]) {
                sh("gcloud auth print-access-token | sudo docker login -u oauth2accesstoken --password-stdin https://asia-east1-docker.pkg.dev")
                sh("docker -t asia-east1-docker.pkg.dev/mypoc-374706/apps-repo/java-app:${env.BUILD_NUMBER} .")
                sh("docker push asia-east1-docker.pkg.dev/mypoc-374706/apps-repo/java-app:${env.BUILD_NUMBER}")
                }
             }
        }
    }    
}
