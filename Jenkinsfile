pipeline {
    agent any
    stages {
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
