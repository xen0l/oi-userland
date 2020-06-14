properties([pipelineTriggers([githubPush()])])

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
            failure {
               setGitHubPullRequestStatus state: "FAILURE"        
            }
         }
      }
   }
}
