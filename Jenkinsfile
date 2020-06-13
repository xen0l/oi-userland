pipeline {
   agent any

   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
            
         }
      }
      post  {
         githubPRComment comment: githubPRMessage('Build ${BUILD_NUMBER} ${BUILD_STATUS}')         
      }
   }
}
