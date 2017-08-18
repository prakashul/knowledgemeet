properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '30', artifactNumToKeepStr: '10', daysToKeepStr: '180', numToKeepStr: '120')), disableConcurrentBuilds(), parameters([string(defaultValue: 'staging', description: '', name: 'branch')]), pipelineTriggers([])])
pipeline {
	agent any
environment {

git_repo_credential_token = 'd60cc6087e37205c8813e95f004597a926813e0e'
git_repo_url = 'https://github.com/prakashul/knowledgemeet.git'
}
stages {

  stage ('Workspace Cleanup') {
    steps {
    deleteDir()
	}
  }
      
  stage ('SCM Checkout') {
	steps {
    git branch: branch, credentialsId: git_repo_credential_token, url: git_repo_url
  }}

  stage ('Branch Checkout') {
    steps {
    sh 'git checkout '+env.branch
    sh 'cat file.txt'
  }}

  stage ('Build Artifact') {
    steps {
    sh 'echo Building Artifact'
  }}

  stage ('Push Artifact') {
	when {
		env.branch 'staging' }
	steps {
    	sh 'echo Pushing Artifact As Branch given is staging' 
         }
 	
	try { 
	timeout(time: 20, unit: 'SECONDS') {
	input 'Do you want to proceed to the Deployment?'
	}
  }
	catch(err) {
    		err.printStackTrace()
    						} 
		sh 'echo Proceeding'
}

stage ('Deploy') {
  steps {
			sh 'echo Deploying'
		 }
}}
}
