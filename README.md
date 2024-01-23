Jenkinsfile 


pipeline {
    agent any

    environment {
        GIT_REPO_URL = 'https://github.com/namratasgit/pipeline1.git'
        NGINX_PATH = 'C:\\Users\\user\\Desktop\\Namrata_Das_PU\\Fall_AY_2023-24\\DevOps\\installers\\nginx-1.24.0\\htmldocs'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Use the checkout step to clone the Git repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: GIT_REPO_URL]]])
                }
            }
        }

        stage('Deploy to Nginx') {
            steps {
                script {
                    // Using the Jenkins workspace variable to reference files
                    bat 'xcopy /y "C:\\Users\\user\\Desktop\\Namrata_Das_PU\\Fall_AY_2023-24\\Subject_Handled\\DevOps\\pipeline\\index.html" "%NGINX_PATH%"'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded! You can add additional steps here.'
        }
        failure {
            echo 'Pipeline failed! You may want to take some actions.'
        }
    }
}


scripted pipeline
command-line shell as given-
node{
stage('Compile'){
		echo "Compiled Successfully!!";
	}

stage('JUnit') {
		echo "JUnit Passed Succesfully!";
}

stage('Quality-Gate') {
		echo "SonarQube Quality Gate passed succesfully!!";
						/*sh exit ("1");*/
}

stage('Deploy') {
		echo "Pass!";
}
}

 descriptvie pipeline

 pipeline {
	agent any
	stages {
		stage('Git-Checkout'){
			steps {
				echo "Checking out from Git Repo";
			}
		}

		stage('Build') {
			steps {
				echo "Building the checkedout project!";
			}
		}

		stage('Unit-Test') {
			steps {
				echo "Running JUnit tests";
			}
		}
		stage('Quality-Gate') {
			steps {
				echo "Verifying Quality Gates";
			}
		}

		stage('Deploy') {
			steps {
				echo "Deploying to stage environments for more tests";
			}
		}
	}
	
		post {
			always {
					echo 'This will always run'
				}
			success {
					echo 'This will run only if successful'
				}
			failure {
					echo 'This will run only if failed'
				}
			unstable {
					echo 'This will run only if the run was marked as unstable'
				}
	    		changed {
					echo 'This will run only if the state of the pipeline has changed'
					echo 'For example, if the pipeline was previously failing but is now successful'
				}
   		 }
}
