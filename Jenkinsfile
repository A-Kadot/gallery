pipeline {
   agent any
   tools {
       nodejs '20.6.1'
   }
post {
        failure {
            mail to: 'weruannn@gmail.com',
                 subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                 body: "Something is wrong with ${env.BUILD_NUMBER}"
        }
    }
   stages {
       stage('Clone Repo'){
           steps{
               git 'https://github.com/A-Kadot/gallery.git'
           }
       }
       stage('install dependancies'){
           steps{
               sh 'npm install'
               sh 'npm install express'
           }
       }
       stage('Run Tests') {
          steps {
            sh 'npm test'
          }
       }
	    stage('Deploy to Render') {
          steps {
            script {
            def renderCommand = "render deploy"
            def renderOptions = [
                "--build-env NODE_ENV=production",
                "--env VAR_NAME=value",  // Add any e
				nvironment variables required
                "--branch main",  // Specify the Git branch to deploy from
                "--name my-render-service",  // Replace with your Render service name
                "--auto-deploy",  // Automatically deploy when changes are pushed
                "--wait",  // Wait for the deployment to complete
            ]
          }
       }
        stage('notify slack') {
          steps {
            slackSend color: 'good', message: "id ${env.BUILD_NUMBER} https://app.slack.com/services/T0101L740P4/B05T5T3GZ97/3ahAtPoUNCmTBejS1RLflyrk", sendAsText: true
          }
       }

   }
}
