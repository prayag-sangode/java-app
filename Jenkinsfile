pipeline {
    agent any
    stages {
       stage("Generating OIDC token and saving it to a file") {
            steps {
                script {
                        sh (script: 'gcloud auth print-identity-token GCP-SA@mypoc-374706.iam.gserviceaccount.com  --audiences="//iam.googleapis.com/projects/512447805963/locations/global/workloadIdentityPools/test-jenkins/providers/jenkins"  > /usr/share/token/key',returnStdout: true)
                }
            }
        }
        stage ("getting the WIF config file into a variable")
        {
            steps {
                     withCredentials([file(credentialsId: 'wif-config-file', variable: 'WIF')]) 
                        {
                         sh '''
                            gcloud auth login --brief --cred-file=$WIF --quiet
                            gcloud container clusters list
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}
