pipeline {
    agent any
    stages {
       stage ("getting the WIF config file into a variable")
        {
            steps {
                     withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'gcp-auth')]) 
                        {
                         sh '''
                            gcloud version
                            gsutil ls
                            gcloud container clusters list
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}
