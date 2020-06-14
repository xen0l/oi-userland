pipeline {
   agent any

   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
         }
         post {
            success {
               setGitHubPullRequestStatus state: "SUCCESS"
            }
            fail {
               setGitHubPullRequestStatus state: "FAILURE"        
            }
         }
      }
   }
}
