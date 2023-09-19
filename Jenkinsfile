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
        sh 'curl --request POST --url https://gallery-z1rp.onrender.com'
       }
		 }
        stage('slack notification') {
          steps {
            slackSend color: 'good', message: "id ${env.BUILD_NUMBER} Hello", sendAsText: true
          }
       }
}
