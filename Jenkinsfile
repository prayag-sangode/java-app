pipeline {
    agent any
    stages {
        stage ("Authenticating to GCP and execute gcloud")
        {
            steps {
                    script
                        {
                         sh '''
                         export 
                            gcloud auth login --brief --cred-file=/usr/share/token/clientLibraryConfig-provider --quiet --project=mypoc-374706
                            gcloud container clusters list
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}
