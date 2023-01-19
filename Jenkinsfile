pipeline {
    agent any
    stages {
         stage ("Docker Login, Build & Push")
            {
            steps {
             withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')])
                {
                sh("gcloud auth activate-service-account --key-file=${GC_KEY}") 
                sh("gsutil ls") 
                sh("gcloud compute instances list")
                sh("1gcloud auth print-access-token | sudo docker login -u oauth2accesstoken --password-stdin https://asia-east1-docker.pkg.dev")
                sh("1gcloud auth configure-docker asia-east1-docker.pkg.dev")
                sh("1sudo docker build -t asia-east1-docker.pkg.dev/pune-powerhouse/apps-repo/java-app:${env.BUILD_NUMBER} .")
                sh("1sudo docker push asia-east1-docker.pkg.dev/pune-powerhouse/apps-repo/java-app:${env.BUILD_NUMBER}")
                }
             }
        }
        stage ("Helm App Deployment")
            {
            steps {
             withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')]) {
                sh("1sed -i 's|asia-east1-docker.pkg.dev/pune-powerhouse/apps-repo/java-app:.*|asia-east1-docker.pkg.dev/pune-powerhouse/apps-repo/java-app:${env.BUILD_NUMBER}|' ./charts/templates/deployment.yaml ")
                sh("1gcloud container clusters get-credentials gke-cluster --zone asia-east1-b --project pune-powerhouse")
                sh("1cat ./charts/templates/deployment.yaml")
                sh("1helm upgrade java-app ./charts --install --values=./charts/values.yaml")
                }
             }
        }
    }    
}
