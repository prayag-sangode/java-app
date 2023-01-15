pipeline {
    agent any
    stages {
       stage("Generating OIDC token and saving it to a file") {
            steps {
                     withCredentials([file(credentialsId: 'wif-config-file', variable: 'WIF')]) 
                script {
                        sh (script: 'gcloud auth print-identity-token GCP-SA@mypoc-374706.iam.gserviceaccount.com  --audiences="//iam.googleapis.com/projects/264743567458/locations/global/workloadIdentityPools/jenkins-wif-pool1/providers/jenkins1"  > /usr/share/token/key',returnStdout: true)
                }
            }
        }
        stage ("getting the WIF config file into a variable")
        {
            steps {
                     withCredentials([file(credentialsId: 'wif-config-file', variable: 'WIF')]) 
                        {
                         sh '''
                            export GOOGLE_APPLICATION_CREDENTIALS=/usr/share/token/key
                            gcloud auth login --brief --cred-file=$WIF --quiet
                            gcloud container clusters list
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}
