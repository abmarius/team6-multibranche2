pipeline {
   agent any
   stages {
       stage('Build Code') {
           steps {
               sh "echo "Building Artifact"
           }
       }
      stage('Deploy Code') {
        when {
            branch 'main'
            }
          steps {
               sh "echo "Deploying Code"
          }
      }
   }
}


