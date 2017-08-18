properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '30', artifactNumToKeepStr: '10', daysToKeepStr: '180', numToKeepStr: '120')), disableConcurrentBuilds(), parameters([string(defaultValue: 'production', description: '', name: 'branch'), string(defaultValue: '$BUILD_ID', description: '', name: 'tag')]), pipelineTriggers([])])

node {
  currentBuild.result = "SUCCESS"

git_repo_credential_token="d60cc6087e37205c8813e95f004597a926813e0e"
git_repo_url="https://github.com/prakashul/knowledgemeet.git"


  stage ('Workspace Cleanup') {
    deleteDir()
  }
      
  stage ('SCM Checkout') {
    git branch: branch, credentialsId: git_repo_credential_token, url: git_repo_url
  }

  stage ('Branch Checkout') {
    sh 'git checkout '+env.branch
    sh 'cat file.txt'
  }
  stage ('Build Artifact') {
    sh 'echo Building Artifact'
  }

  stage ('Push Artifact') {
    if ( env.branch == 'staging') { 
    sh 'echo Pushing Artifact As Branch given is staging' 
         }
	else {
		sh 'echo Skipping Stage as branch is not staging'
             }
	input 'Do you want to proceed to the Deployment?'
  }

stage ('Deploy') {
		 build job: 'Deploy', propagate: false
			sh 'echo Deploying'
		 }
}
