pipeline {
   agent any

   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
            githubPRComment comment: githubPRMessage('Build ${BUILD_NUMBER} ${BUILD_STATUS}')
         }
      }
   }
}
