pipeline {
    agent any
    stages {
       stage ("getting the WIF config file into a variable")
        {
            steps {
             withCredentials([file(credentialsId: 'gcp-auth-id', variable: 'GC_KEY')]) {
                sh("gcloud auth activate-service-account --key-file=${GC_KEY}")
                sh("gsutil ls")
  }
                }
        }
    }    
}
