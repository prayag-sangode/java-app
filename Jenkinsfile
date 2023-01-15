pipeline {
    agent any
    stages {
       stage ("Git Checkout")
        {
            steps {
                     checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/prayag-sangode/java-app.git']])
                }
        }
                
       stage ("getting the WIF config file into a variable")
        {
            steps {
                     withCredentials([file(credentialsId: 'wif-config-file', variable: 'WIF')]) 
                        {
                         sh '''
                            gcloud auth login --brief --cred-file=$WIF --quiet
                            gcloud compute instances list
                            '''

                        }
                }
        }
    }    
}

