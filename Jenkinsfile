pipeline {
    agent any	
    stages {
	stage('SCMCheckout') {
            steps {
		    // Source branch checkout
		   git branch: 'source-1', credentialsId: 'e6f63267-7132-498f-8496-96730d4d8bd7', url: 'https://github.com/valentinenuma/test-jenkins-pipeline.git'		    
            }
        }
	stage('CreateBranch') {
            steps {
		    withCredentials([gitUsernamePassword(credentialsId: 'e6f63267-7132-498f-8496-96730d4d8bd7', gitToolName: 'Default')]) {			    			    
			    sh "git fetch origin"			    
			    // Get updated changes from source branch
			    sh "git pull --force origin source-1"
			    sh "git config --global push.default matching"
			    // Delete local branch  if exist
			    sh "git branch -D release-1"
			    // Delete remote branch if exist
			    sh "git push --delete origin release-1"
			    // Destination Branch, Build will be created from this branch
			    sh "git checkout -b release-1"
			    sh "git push -u origin release-1"
			    
			    // Merge release-1 branch into 'main' (destination)
			    sh "git checkout destination"			    
			    sh "git merge origin/release-1"	
			   
			    			    
		    }		    
            }
        }	  
        stage('Build') {
            steps {		    
		    echo "Build stage"
            }
        }
    }
}
