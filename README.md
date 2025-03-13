# pipeline
Simple Pipeline:
pipeline {
	agent any
	stages {
		stage ('stage 1') {
			steps {
				echo "This is stage 1"
			}
		}
		stage ('stage 2') {
			steps {
				echo "This is stage 2"
			}
		}
	}
}
CICD Pipeline:

pipeline {
	agent any
	stages {
		stage ('SCM Checkout') {
			steps {
				echo "This is Git checkout stage"
				sh 'sleep 5'
			}
		}
		stage ('Build') {
			steps {
				echo "This is Build stage"
				sh 'sleep 5'
			}
		}
		stage ('Push') {
			steps {
				echo "This is Artifactory Push stage"
				sh 'sleep 5'
			}
		}
		stage ('Deploy') {
			steps {
				echo "This is Deployment stage"
				sh 'sleep 5'
			}
		}
	}
}
-------------------------------------------------------------------------------------------------------------
Im̲p̲o̲r̲t̲a̲n̲t̲ Q̲u̲e̲s̲t̲i̲o̲n̲s̲ F̲r̲o̲m̲ J̲e̲n̲k̲i̲n̲s̲ -̲
1.	How to integrate Jenkins with GitHub
2.	Integration with SonarQube
3.	How to authorize user / security related question
4.	How to run multiple jobs parallelly in Jenkins
5.	What is agent.
6.	How to take backup of Jenkins.






Pipeline with Agents:

pipeline {
	agent none
	stages {
		stage ('stage 1') {
			agent {label 'master'}
			steps {
				echo "This is stage 1"
				sh 'sleep 10'
			}
		}
		stage ('stage 2') {
			agent {label 'java'}
			steps {
				echo "This is stage 2"
				sh 'sleep 10'
			}
		}
	}
}
--------------------------------------------------------------------------------------------------------------

pipeline {
	agent none
	stages {
		stage ('stage 1') {
			agent {label 'java'}
			steps {
				sh 'cd directory'
				sh 'git clone repo'
				sh 'cd directory'
				sh 'mvn clean install'
			}
		}
		stage ('stage 2') {
			agent {label 'java'}
			steps {
				sh 'cp .war to tomcat webapps'
			}
		}
	}
}
--------------------------------------------------------------------------------------------------------------

Parallel Stages:

pipeline {
    agent any
    stages {
		stage("STAGE 1"){
            			steps {
                			echo "This is stage one"
               				 sh 'sleep 5'
           			 }
        		}
		stage("STAGE 2"){
			parallel {		
				stage("STAGE 2 A"){
					steps {
						echo "This is stage 2A"
						sh 'sleep 5'
					}
				}
				stage("STAGE 2 B"){
					steps {
						echo "This is stage 2B"
						sh 'sleep 5'
	                }
				}
			}
		}
		stage("STAGE 3"){
            			steps {
                			echo "This is stage three"
                			sh 'sleep 5'
           			 }
       		 }
    }    
}
--------------------------------------------------------------------------------------------------------------









Parallel Steps:

pipeline {
    agent any
    triggers {
		pollSCM '* * * * *'
	}
	stages {
		stage("STAGE 1"){
			steps {
				parallel (
					step1: {	
						echo "This is stage 1 step 1"
						sh 'sleep 5'
				    },
					step2: {
						echo "This is stage 1 step 2"
						sh 'sleep 5'
				    },
					step3: {
						echo "This is stage 1 step 3"
						sh 'sleep 5'
				    }
			   )
			}
		}
			
		stage("STAGE 2"){
			steps {
				echo "This is stage one"
				sh 'sleep 5'
			}
		}
    }    
}
