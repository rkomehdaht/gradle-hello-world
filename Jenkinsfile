pipeline{
    agent {
        label 'slave1'
    }
    tools {
        gradle 'gradle4'
    }
    stages{
		stage ('Checkout'){
            steps{
      			checkout scm  
            } 
   		}
   		stage ('build'){
            steps{
      	        sh "gradle build"
            }
   		}
        stage ('Unit-test'){
            steps{
                sh "gradle test"
            }
        }
        stage ('Func-test'){
            parallel{
                stage ('Test1'){
                    steps{
                        sh "sh test-data/int-test.sh 'build/libs/oto-gradle-1.0.jar' 'otoMato' 'Hello Otomato!'"
                    }
                }
                stage ('Test2'){
                    steps{
                        sh "sh test-data/int-test.sh 'build/libs/oto-gradle-1.0.jar' 'ruslan' 'Hello Ruslan!'"
                    }
                }
                stage ('Test3'){
                    steps{
                        sh "sh test-data/int-test.sh 'build/libs/oto-gradle-1.0.jar' 'piatrovich' 'Hello Piatrovich!'"
                    }
                }
            }
        }

    }
    post{
        success {
            addBadge(icon: 'completed.gif', text: 'OK')
        }
        failure {
            addBadge(icon: 'error.gif', text: 'Error')
        }
        always {
            archiveArtifacts 'build/test-results/junit-platform/*.xml'
	    junit 'build/test-results/junit-platform/*.xml'
        }
    }
}
