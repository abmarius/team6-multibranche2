pipeline {
   agent any
   stages {
       stage('Build Code') {
           steps {
               sh "echo "Building Artifact"
           }
       }
      stage('Deploy Code') {
          steps {
               sh "echo "Deploying Code"
          }
      }
   }
}


Jenkinsfile2:
pipeline {
    agent any
    stages {
        stage('Main Branch Deploy Code') {
            when {
                branch 'main'
            }
            steps {
                sh 'echo "Building Artifact from Main branch"'
 
                sh 'echo "Deploying Code from Main branch"'
            }
        }
        stage('Develop Branch Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh 'echo "Building Artifact from Develop branch"'
                sh 'echo "Deploying Code from Develop branch"'
           }
        }
    }
}


pipeline {
    agent any
    tools {
        maven 'MAVEN_PATH'
        jdk 'jdk8'
    }
    stages {
        stage("Tools initialization") {
            steps {
                sh "mvn --version"
                sh "java -version"
            }
        }
        stage("Checkout Code") {
            steps {
                checkout scm
            }
        }
        stage("Check Code Health") {
            when {
                not {
                    anyOf {
                        branch 'master';
                        branch 'develop'
                    }
                }
           }
           steps {
               sh "mvn clean compile"
            }
        }
        stage("Run Test cases") {
            when {
                branch 'develop';
            }
           steps {
               sh "mvn clean test"
            }
        }
        stage("Check Code coverage") {
            when {
                branch 'develop'
            }
            steps {
               jacoco(
                    execPattern: '**/target/**.exec',
                    classPattern: '**/target/classes',
                    sourcePattern: '**/src',
                    inclusionPattern: 'com/iamvickyav/**',
                    changeBuildStatus: true,
                    minimumInstructionCoverage: '30',
                    maximumInstructionCoverage: '80')
           }
        }
        stage("Build & Deploy Code") {
            when {
                branch 'master'
            }
            steps {
                sh "mvn tomcat7:deploy"
            }
        }
    }
 }
=============================================================================================================

pipeline{
  agent any
  stages{
  	stage('version-control'){
  		steps{
  			git checkout
  		}
  	}
    stage('parallel-job'){
      parallel{
        stage('sub-job1'){
          steps{
            echo 'action1'
          }
        }
        stage('sub-job2'){
          steps{
            echo 'action2'
          }
        }
      }
    }
    stage('codebuild'){
    	steps{
    		sh 'cat /etc/passwd'
    	}
    }
  }
}

techops-3050

pipeline{
	agent { 'master1'}
	tools { maven 'maven'
            Ansible 'ansible'
}
stages{
	agent node1
	stage('git-clone'){
		steps{
			action1
		}
	}
	agent node2
	stage('code-build'){
		steps{
			action2
		}
	}
}
}
=================================================================================================

pipeline{
	agent any 
	stages{
		stage('1-codecheckout'){
			steps{
				git clone
			}
		}
		stage('2-codebuild'){
			when {
				branch 'main'
			}
			steps{
				sh 'git version'
			}

		}
		stage('3-deployment'){
			when {
				branch 'develop'
			}
			steps{
				sh 'mvn deploy'
			}
		}
	}
}
